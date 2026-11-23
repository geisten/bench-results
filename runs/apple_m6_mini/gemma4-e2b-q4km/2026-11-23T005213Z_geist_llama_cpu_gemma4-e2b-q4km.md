# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `b90b6b27c840`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 541.67 ± 1.59 | 283.49 ± 0.11 | +91.07% | 71.69 ± 0.09 | 65.43 ± 0.04 | +9.57% |
| 256 | 712.57 ± 0.43 | 280.10 ± 0.15 | +154.40% | 69.58 ± 0.05 | 62.91 ± 0.06 | +10.61% |
| 512 | 819.82 ± 1.04 | 275.06 ± 0.56 | +198.05% | 66.02 ± 0.10 | 61.56 ± 0.04 | +7.24% |
| 1024 | 856.46 ± 0.34 | 260.43 ± 0.69 | +228.87% | 63.47 ± 0.10 | 59.63 ± 0.07 | +6.44% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
