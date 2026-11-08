# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 250.61 ± 0.65 | 213.36 ± 0.24 | +17.46% | 53.31 ± 0.04 | 55.99 ± 0.15 | -4.79% |
| 256 | 245.96 ± 0.08 | 212.96 ± 0.11 | +15.50% | 51.87 ± 0.04 | 51.96 ± 0.12 | -0.17% |
| 512 | 236.21 ± 0.09 | 210.97 ± 0.54 | +11.96% | 49.17 ± 0.06 | 49.07 ± 0.26 | +0.21% |
| 1024 | 217.87 ± 0.10 | 201.69 ± 0.84 | +8.02% | 44.05 ± 0.09 | 43.44 ± 0.39 | +1.41% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
