# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `aeb3a50153d7`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 33.55 ± 0.02 | 21.46 ± 0.03 | +56.34% | 13.22 ± 0.02 | 0.78 ± 0.00 | +1588.21% |
| 256 | 33.42 ± 0.03 | 27.83 ± 0.07 | +20.08% | 13.13 ± 0.02 | 0.78 ± 0.00 | +1577.95% |
| 512 | 33.23 ± 0.03 | 32.35 ± 0.04 | +2.71% | 12.96 ± 0.01 | 0.78 ± 0.00 | +1557.46% |
| 1024 | 32.75 ± 0.02 | 32.19 ± 0.03 | +1.75% | 12.63 ± 0.02 | 0.78 ± 0.00 | +1517.83% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
