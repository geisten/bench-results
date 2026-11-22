# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 249.77 ± 0.19 | 213.44 ± 0.14 | +17.02% | 53.85 ± 0.04 | 56.79 ± 0.03 | -5.17% |
| 256 | 244.99 ± 0.17 | 212.93 ± 0.04 | +15.06% | 52.36 ± 0.04 | 52.72 ± 0.04 | -0.67% |
| 512 | 235.32 ± 0.08 | 211.18 ± 0.56 | +11.43% | 49.56 ± 0.06 | 49.75 ± 0.13 | -0.37% |
| 1024 | 217.09 ± 0.13 | 201.73 ± 0.78 | +7.61% | 44.29 ± 0.07 | 44.27 ± 0.13 | +0.05% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
