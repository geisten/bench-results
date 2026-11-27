# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `f4ae43569c6a`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 280.72 ± 0.47 | 235.57 ± 0.24 | +19.17% | 18.93 ± 0.01 | 15.76 ± 0.03 | +20.06% |
| 256 | 280.13 ± 0.29 | 236.78 ± 0.14 | +18.31% | 18.88 ± 0.01 | 15.74 ± 0.01 | +19.94% |
| 512 | 279.88 ± 0.19 | 234.06 ± 0.20 | +19.58% | 18.84 ± 0.01 | 15.65 ± 0.01 | +20.40% |
| 1024 | 286.52 ± 0.16 | 232.52 ± 0.27 | +23.22% | 18.72 ± 0.01 | 15.60 ± 0.02 | +19.96% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
