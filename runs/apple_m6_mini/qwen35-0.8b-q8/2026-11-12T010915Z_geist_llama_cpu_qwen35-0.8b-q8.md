# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 986.52 ± 1.61 | 917.68 ± 3.23 | +7.50% | 142.60 ± 0.15 | 134.30 ± 0.46 | +6.18% |
| 256 | 980.40 ± 1.23 | 901.71 ± 9.34 | +8.73% | 141.56 ± 0.16 | 132.05 ± 0.48 | +7.20% |
| 512 | 965.14 ± 2.28 | 888.38 ± 3.60 | +8.64% | 139.33 ± 0.25 | 131.28 ± 0.40 | +6.13% |
| 1024 | 934.68 ± 1.56 | 856.66 ± 6.94 | +9.11% | 134.40 ± 0.32 | 129.03 ± 0.36 | +4.17% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
