# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 178.01 ± 0.09 | 142.76 ± 0.04 | +24.69% | 36.49 ± 0.02 | 34.29 ± 0.08 | +6.43% |
| 256 | 176.06 ± 0.13 | 141.78 ± 0.43 | +24.18% | 35.85 ± 0.06 | 33.48 ± 0.05 | +7.09% |
| 512 | 171.80 ± 0.17 | 142.19 ± 0.50 | +20.83% | 34.84 ± 0.07 | 32.98 ± 0.06 | +5.64% |
| 1024 | 166.55 ± 0.36 | 137.09 ± 0.62 | +21.48% | 34.12 ± 0.08 | 32.28 ± 0.07 | +5.68% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
