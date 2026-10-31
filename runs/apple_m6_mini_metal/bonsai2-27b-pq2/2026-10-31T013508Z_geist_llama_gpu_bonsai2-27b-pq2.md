# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `93817e73fce2`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 93.34 ± 0.01 | 235.31 ± 0.28 | -60.33% | 19.04 ± 0.01 | 16.21 ± 0.04 | +17.49% |
| 256 | 95.82 ± 0.01 | 237.16 ± 0.16 | -59.60% | 19.01 ± 0.00 | 16.17 ± 0.04 | +17.55% |
| 512 | 95.90 ± 0.01 | 234.57 ± 0.27 | -59.12% | 18.96 ± 0.01 | 16.07 ± 0.09 | +17.96% |
| 1024 | 95.24 ± 0.01 | 232.46 ± 0.19 | -59.03% | 18.80 ± 0.02 | 15.85 ± 0.10 | +18.61% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
