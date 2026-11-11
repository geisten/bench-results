# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `64c3d9c4227e`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.80 ± 0.39 | 235.25 ± 0.60 | +9.16% | 18.96 ± 0.01 | 16.06 ± 0.01 | +18.06% |
| 256 | 259.79 ± 0.15 | 237.14 ± 0.29 | +9.55% | 18.93 ± 0.00 | 16.04 ± 0.01 | +17.99% |
| 512 | 224.90 ± 0.10 | 234.25 ± 0.20 | -3.99% | 18.88 ± 0.01 | 15.97 ± 0.01 | +18.20% |
| 1024 | 222.44 ± 0.09 | 232.74 ± 0.23 | -4.42% | 18.74 ± 0.01 | 15.90 ± 0.01 | +17.89% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
