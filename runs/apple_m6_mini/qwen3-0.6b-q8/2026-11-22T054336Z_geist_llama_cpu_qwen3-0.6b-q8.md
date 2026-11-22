# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1202.07 ± 1.68 | 1406.14 ± 3.08 | -14.51% | 182.00 ± 0.11 | 190.44 ± 0.27 | -4.43% |
| 256 | 1118.97 ± 0.42 | 1364.79 ± 0.72 | -18.01% | 166.23 ± 0.32 | 162.21 ± 0.43 | +2.48% |
| 512 | 966.51 ± 0.81 | 1253.30 ± 2.73 | -22.88% | 141.67 ± 0.18 | 142.15 ± 0.49 | -0.34% |
| 1024 | 758.44 ± 0.31 | 1065.85 ± 0.93 | -28.84% | 109.10 ± 0.32 | 108.03 ± 0.79 | +0.99% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
