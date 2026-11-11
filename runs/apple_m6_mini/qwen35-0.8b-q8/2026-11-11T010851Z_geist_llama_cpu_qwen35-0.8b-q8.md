# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 992.73 ± 1.20 | 920.32 ± 2.69 | +7.87% | 142.94 ± 0.23 | 133.23 ± 0.70 | +7.28% |
| 256 | 987.01 ± 2.24 | 906.92 ± 5.37 | +8.83% | 141.96 ± 0.16 | 131.45 ± 0.29 | +7.99% |
| 512 | 973.40 ± 0.76 | 891.69 ± 0.94 | +9.16% | 139.77 ± 0.26 | 130.09 ± 0.25 | +7.44% |
| 1024 | 940.16 ± 2.00 | 869.19 ± 1.31 | +8.17% | 134.98 ± 0.08 | 128.25 ± 0.33 | +5.25% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
