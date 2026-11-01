# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1205.28 ± 0.73 | 1405.78 ± 1.17 | -14.26% | 181.99 ± 0.19 | 191.37 ± 0.35 | -4.90% |
| 256 | 1121.63 ± 1.14 | 1364.99 ± 0.67 | -17.83% | 166.24 ± 0.29 | 163.64 ± 0.36 | +1.58% |
| 512 | 967.40 ± 0.62 | 1254.70 ± 2.02 | -22.90% | 141.45 ± 0.34 | 144.51 ± 0.66 | -2.12% |
| 1024 | 758.99 ± 0.35 | 1065.94 ± 0.94 | -28.80% | 108.55 ± 0.77 | 109.19 ± 2.46 | -0.59% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
