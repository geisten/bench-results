# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.95 ± 0.27 | 283.66 ± 0.11 | +27.25% | 72.50 ± 0.04 | 65.50 ± 0.16 | +10.69% |
| 256 | 354.44 ± 1.30 | 280.44 ± 0.09 | +26.39% | 70.33 ± 0.05 | 62.96 ± 0.12 | +11.72% |
| 512 | 340.92 ± 0.15 | 275.75 ± 0.31 | +23.63% | 66.73 ± 0.09 | 61.57 ± 0.21 | +8.39% |
| 1024 | 322.51 ± 0.49 | 261.08 ± 0.72 | +23.53% | 64.13 ± 0.11 | 59.69 ± 0.24 | +7.44% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
