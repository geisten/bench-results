# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 990.44 ± 0.78 | 926.76 ± 2.07 | +6.87% | 142.48 ± 0.20 | 135.62 ± 0.33 | +5.06% |
| 256 | 985.12 ± 0.60 | 906.89 ± 3.46 | +8.63% | 141.49 ± 0.15 | 133.65 ± 0.09 | +5.86% |
| 512 | 972.37 ± 0.50 | 887.48 ± 4.66 | +9.57% | 139.26 ± 0.14 | 132.43 ± 0.20 | +5.15% |
| 1024 | 939.04 ± 0.98 | 864.17 ± 5.37 | +8.66% | 134.67 ± 0.05 | 130.43 ± 0.22 | +3.25% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
