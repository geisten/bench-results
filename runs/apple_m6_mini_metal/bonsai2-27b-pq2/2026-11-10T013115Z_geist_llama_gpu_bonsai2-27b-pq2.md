# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `29a0ce4b5937`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 256.38 ± 0.49 | 234.96 ± 0.36 | +9.12% | 18.91 ± 0.01 | 16.00 ± 0.01 | +18.16% |
| 256 | 260.27 ± 0.35 | 236.85 ± 0.23 | +9.89% | 18.89 ± 0.01 | 15.99 ± 0.01 | +18.11% |
| 512 | 224.81 ± 0.11 | 234.19 ± 0.14 | -4.01% | 18.83 ± 0.01 | 15.91 ± 0.01 | +18.32% |
| 1024 | 222.34 ± 0.20 | 232.61 ± 0.20 | -4.41% | 18.70 ± 0.02 | 15.85 ± 0.01 | +17.99% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
