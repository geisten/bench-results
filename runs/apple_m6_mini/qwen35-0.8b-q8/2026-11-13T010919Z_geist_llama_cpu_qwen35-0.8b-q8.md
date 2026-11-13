# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 971.96 ± 8.23 | 923.55 ± 5.03 | +5.24% | 139.01 ± 0.25 | 133.33 ± 0.25 | +4.26% |
| 256 | 970.92 ± 1.99 | 904.84 ± 5.65 | +7.30% | 137.81 ± 0.28 | 131.56 ± 0.37 | +4.75% |
| 512 | 953.56 ± 4.37 | 892.03 ± 1.57 | +6.90% | 135.85 ± 0.20 | 130.69 ± 0.61 | +3.95% |
| 1024 | 923.90 ± 2.31 | 870.47 ± 1.41 | +6.14% | 131.55 ± 0.22 | 128.51 ± 0.49 | +2.37% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
