# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `ff31d42364e1`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.72 ± 0.52 | 235.82 ± 0.56 | +8.86% | 19.02 ± 0.01 | 16.23 ± 0.01 | +17.15% |
| 256 | 259.86 ± 0.22 | 237.53 ± 0.15 | +9.40% | 18.98 ± 0.01 | 16.21 ± 0.01 | +17.08% |
| 512 | 224.96 ± 0.13 | 234.25 ± 0.57 | -3.97% | 18.94 ± 0.01 | 16.14 ± 0.01 | +17.37% |
| 1024 | 222.46 ± 0.10 | 233.33 ± 0.25 | -4.66% | 18.80 ± 0.01 | 16.07 ± 0.01 | +17.02% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
