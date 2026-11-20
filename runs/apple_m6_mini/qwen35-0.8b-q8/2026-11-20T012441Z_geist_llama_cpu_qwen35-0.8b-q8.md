# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 991.35 ± 0.52 | 922.43 ± 2.96 | +7.47% | 142.41 ± 0.11 | 135.01 ± 0.19 | +5.49% |
| 256 | 986.46 ± 0.69 | 901.69 ± 6.99 | +9.40% | 141.45 ± 0.13 | 133.13 ± 0.12 | +6.25% |
| 512 | 971.90 ± 0.99 | 883.42 ± 3.53 | +10.01% | 139.32 ± 0.13 | 131.76 ± 0.17 | +5.74% |
| 1024 | 939.27 ± 0.73 | 854.72 ± 2.45 | +9.89% | 134.45 ± 0.09 | 129.76 ± 0.13 | +3.61% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
