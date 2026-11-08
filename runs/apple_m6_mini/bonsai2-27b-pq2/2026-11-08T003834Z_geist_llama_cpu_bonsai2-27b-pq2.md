# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `ff31d42364e1`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 33.44 ± 0.08 | 21.59 ± 0.03 | +54.91% | 13.12 ± 0.04 | 0.78 ± 0.00 | +1575.01% |
| 256 | 33.38 ± 0.06 | 27.95 ± 0.03 | +19.45% | 13.01 ± 0.03 | 0.78 ± 0.00 | +1562.44% |
| 512 | 33.18 ± 0.03 | 32.55 ± 0.04 | +1.94% | 12.84 ± 0.03 | 0.78 ± 0.00 | +1542.55% |
| 1024 | 32.74 ± 0.03 | 32.42 ± 0.03 | +0.99% | 12.51 ± 0.03 | 0.78 ± 0.00 | +1501.71% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
