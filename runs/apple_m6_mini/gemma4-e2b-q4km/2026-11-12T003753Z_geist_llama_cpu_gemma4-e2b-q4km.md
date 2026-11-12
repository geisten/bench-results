# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.00 ± 0.27 | 283.69 ± 0.13 | +27.25% | 72.14 ± 0.17 | 66.14 ± 0.21 | +9.06% |
| 256 | 353.85 ± 0.36 | 280.42 ± 0.26 | +26.19% | 70.18 ± 0.07 | 63.62 ± 0.13 | +10.31% |
| 512 | 340.60 ± 0.34 | 275.38 ± 0.65 | +23.68% | 66.59 ± 0.07 | 62.29 ± 0.18 | +6.90% |
| 1024 | 322.04 ± 0.15 | 261.01 ± 0.58 | +23.38% | 63.96 ± 0.12 | 60.25 ± 0.15 | +6.16% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
