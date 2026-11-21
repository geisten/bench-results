# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `aeb3a50153d7`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 255.76 ± 0.33 | 234.24 ± 0.37 | +9.19% | 18.72 ± 0.00 | 15.65 ± 0.01 | +19.59% |
| 256 | 258.69 ± 0.29 | 235.85 ± 0.21 | +9.68% | 18.68 ± 0.00 | 15.64 ± 0.01 | +19.46% |
| 512 | 223.64 ± 0.09 | 232.25 ± 0.39 | -3.71% | 18.63 ± 0.00 | 15.57 ± 0.01 | +19.69% |
| 1024 | 221.14 ± 0.04 | 230.79 ± 0.33 | -4.18% | 18.51 ± 0.00 | 15.51 ± 0.01 | +19.32% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
