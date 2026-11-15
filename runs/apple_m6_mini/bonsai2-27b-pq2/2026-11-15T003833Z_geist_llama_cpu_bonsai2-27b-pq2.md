# Current CPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `7765b16fc97f`; llama.cpp `adfffbe41b2c`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 33.51 ± 0.05 | 21.69 ± 0.02 | +54.48% | 13.10 ± 0.05 | 0.78 ± 0.00 | +1572.82% |
| 256 | 33.41 ± 0.03 | 28.05 ± 0.04 | +19.11% | 13.04 ± 0.04 | 0.78 ± 0.00 | +1566.72% |
| 512 | 33.24 ± 0.03 | 32.63 ± 0.04 | +1.86% | 12.89 ± 0.02 | 0.78 ± 0.00 | +1547.41% |
| 1024 | 32.79 ± 0.03 | 32.53 ± 0.05 | +0.82% | 12.55 ± 0.02 | 0.78 ± 0.00 | +1506.99% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
