# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1002.24 ± 0.31 | 924.44 ± 2.92 | +8.42% | 147.47 ± 0.14 | 136.91 ± 0.09 | +7.71% |
| 256 | 996.77 ± 0.68 | 907.16 ± 7.13 | +9.88% | 146.47 ± 0.12 | 134.76 ± 0.12 | +8.69% |
| 512 | 982.45 ± 0.47 | 890.23 ± 2.45 | +10.36% | 143.66 ± 0.15 | 133.57 ± 0.14 | +7.55% |
| 1024 | 948.61 ± 0.88 | 869.19 ± 2.28 | +9.14% | 138.34 ± 0.12 | 131.49 ± 0.17 | +5.21% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
