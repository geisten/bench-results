# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 250.85 ± 0.08 | 213.42 ± 0.10 | +17.54% | 57.89 ± 0.04 | 56.52 ± 0.11 | +2.43% |
| 256 | 245.97 ± 0.20 | 212.97 ± 0.07 | +15.49% | 56.17 ± 0.03 | 52.18 ± 0.05 | +7.64% |
| 512 | 236.28 ± 0.08 | 211.39 ± 0.29 | +11.78% | 53.12 ± 0.04 | 49.00 ± 0.13 | +8.41% |
| 1024 | 218.14 ± 0.25 | 201.94 ± 0.59 | +8.02% | 47.34 ± 0.04 | 43.20 ± 0.09 | +9.58% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
