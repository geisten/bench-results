# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.68 ± 0.40 | 283.57 ± 0.11 | +27.19% | 71.91 ± 0.07 | 65.58 ± 0.18 | +9.65% |
| 256 | 354.17 ± 0.62 | 280.21 ± 0.18 | +26.39% | 69.88 ± 0.09 | 63.03 ± 0.09 | +10.87% |
| 512 | 340.37 ± 0.31 | 275.15 ± 0.41 | +23.70% | 66.28 ± 0.12 | 61.65 ± 0.09 | +7.52% |
| 1024 | 321.71 ± 0.12 | 260.68 ± 0.36 | +23.41% | 63.70 ± 0.03 | 59.73 ± 0.22 | +6.65% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
