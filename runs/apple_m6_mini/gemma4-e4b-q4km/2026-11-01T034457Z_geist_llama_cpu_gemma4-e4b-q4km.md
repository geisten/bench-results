# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 178.65 ± 0.44 | 142.58 ± 0.07 | +25.29% | 37.10 ± 0.01 | 33.96 ± 0.04 | +9.23% |
| 256 | 176.19 ± 0.12 | 141.82 ± 0.14 | +24.23% | 36.56 ± 0.01 | 33.15 ± 0.02 | +10.27% |
| 512 | 171.97 ± 0.13 | 142.13 ± 0.49 | +20.99% | 35.46 ± 0.04 | 32.62 ± 0.05 | +8.71% |
| 1024 | 167.32 ± 0.15 | 137.03 ± 0.31 | +22.10% | 34.71 ± 0.03 | 32.00 ± 0.02 | +8.48% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
