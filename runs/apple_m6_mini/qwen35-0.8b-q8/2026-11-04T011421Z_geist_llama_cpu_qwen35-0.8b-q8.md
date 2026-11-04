# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 975.14 ± 1.15 | 919.32 ± 0.92 | +6.07% | 135.14 ± 0.23 | 135.36 ± 0.32 | -0.16% |
| 256 | 970.33 ± 1.03 | 907.99 ± 3.70 | +6.87% | 134.47 ± 0.19 | 133.46 ± 0.34 | +0.75% |
| 512 | 959.01 ± 1.32 | 877.44 ± 7.89 | +9.30% | 132.75 ± 0.20 | 132.09 ± 0.16 | +0.50% |
| 1024 | 928.17 ± 2.25 | 853.60 ± 3.79 | +8.74% | 128.32 ± 0.26 | 129.30 ± 0.28 | -0.76% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
