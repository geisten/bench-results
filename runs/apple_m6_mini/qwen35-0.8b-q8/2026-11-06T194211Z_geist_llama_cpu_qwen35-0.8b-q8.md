# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 996.42 ± 0.36 | 924.07 ± 4.29 | +7.83% | 144.37 ± 0.19 | 135.32 ± 0.38 | +6.69% |
| 256 | 990.40 ± 0.81 | 907.43 ± 6.06 | +9.14% | 143.33 ± 0.24 | 133.40 ± 0.17 | +7.44% |
| 512 | 976.68 ± 0.61 | 890.29 ± 2.10 | +9.70% | 140.93 ± 0.15 | 132.26 ± 0.30 | +6.56% |
| 1024 | 943.68 ± 1.31 | 866.33 ± 2.69 | +8.93% | 136.18 ± 0.35 | 130.13 ± 0.34 | +4.65% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
