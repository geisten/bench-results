# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1194.20 ± 2.97 | 1403.67 ± 2.55 | -14.92% | 176.40 ± 0.13 | 186.05 ± 1.33 | -5.19% |
| 256 | 1113.51 ± 1.87 | 1363.95 ± 0.92 | -18.36% | 161.69 ± 0.17 | 159.07 ± 1.45 | +1.65% |
| 512 | 959.15 ± 1.72 | 1254.74 ± 1.88 | -23.56% | 137.77 ± 0.81 | 143.95 ± 0.46 | -4.29% |
| 1024 | 753.93 ± 0.90 | 1065.76 ± 1.30 | -29.26% | 104.99 ± 0.57 | 111.67 ± 4.74 | -5.98% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
