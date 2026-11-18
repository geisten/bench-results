# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `372846765fa0`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 255.88 ± 0.29 | 234.51 ± 0.59 | +9.11% | 18.74 ± 0.01 | 15.71 ± 0.01 | +19.33% |
| 256 | 258.66 ± 0.32 | 236.08 ± 0.32 | +9.57% | 18.71 ± 0.01 | 15.69 ± 0.01 | +19.23% |
| 512 | 223.78 ± 0.12 | 232.66 ± 0.52 | -3.82% | 18.66 ± 0.01 | 15.62 ± 0.01 | +19.46% |
| 1024 | 221.26 ± 0.04 | 230.89 ± 0.29 | -4.17% | 18.53 ± 0.01 | 15.56 ± 0.00 | +19.07% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
