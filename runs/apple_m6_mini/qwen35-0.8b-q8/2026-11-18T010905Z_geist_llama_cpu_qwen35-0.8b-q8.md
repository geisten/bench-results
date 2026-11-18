# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 992.01 ± 0.67 | 923.41 ± 2.61 | +7.43% | 142.07 ± 0.13 | 134.34 ± 0.24 | +5.76% |
| 256 | 985.99 ± 1.00 | 903.71 ± 3.90 | +9.11% | 141.00 ± 0.24 | 132.08 ± 0.23 | +6.75% |
| 512 | 972.60 ± 0.75 | 873.44 ± 11.67 | +11.35% | 138.91 ± 0.15 | 130.82 ± 0.71 | +6.18% |
| 1024 | 938.21 ± 2.17 | 852.99 ± 9.29 | +9.99% | 134.00 ± 0.10 | 128.73 ± 0.37 | +4.09% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
