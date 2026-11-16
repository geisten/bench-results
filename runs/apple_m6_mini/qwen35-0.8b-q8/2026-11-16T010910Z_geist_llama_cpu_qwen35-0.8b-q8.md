# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1003.45 ± 0.88 | 925.22 ± 3.73 | +8.45% | 146.33 ± 0.11 | 135.23 ± 0.14 | +8.21% |
| 256 | 998.18 ± 1.08 | 910.29 ± 3.34 | +9.65% | 144.84 ± 0.21 | 133.03 ± 0.17 | +8.87% |
| 512 | 983.23 ± 0.66 | 885.32 ± 3.19 | +11.06% | 142.44 ± 0.21 | 132.14 ± 0.06 | +7.80% |
| 1024 | 950.22 ± 0.93 | 851.92 ± 7.02 | +11.54% | 137.43 ± 0.14 | 129.92 ± 0.09 | +5.78% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
