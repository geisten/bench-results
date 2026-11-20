# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `aeb3a50153d7`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 255.97 ± 0.27 | 234.87 ± 0.25 | +8.98% | 18.83 ± 0.00 | 15.91 ± 0.02 | +18.37% |
| 256 | 258.49 ± 0.18 | 235.73 ± 0.12 | +9.66% | 18.79 ± 0.01 | 15.87 ± 0.04 | +18.41% |
| 512 | 223.68 ± 0.18 | 232.55 ± 0.31 | -3.81% | 18.75 ± 0.00 | 15.79 ± 0.04 | +18.74% |
| 1024 | 221.16 ± 0.09 | 230.96 ± 0.22 | -4.24% | 18.61 ± 0.01 | 15.71 ± 0.03 | +18.41% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
