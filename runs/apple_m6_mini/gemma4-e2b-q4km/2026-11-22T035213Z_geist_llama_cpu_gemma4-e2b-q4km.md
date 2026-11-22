# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.53 ± 0.29 | 283.38 ± 0.12 | +27.23% | 72.25 ± 0.07 | 65.23 ± 0.16 | +10.77% |
| 256 | 353.71 ± 0.32 | 280.12 ± 0.28 | +26.27% | 70.22 ± 0.10 | 62.76 ± 0.16 | +11.89% |
| 512 | 340.16 ± 0.19 | 274.92 ± 0.55 | +23.73% | 66.59 ± 0.06 | 61.49 ± 0.04 | +8.29% |
| 1024 | 321.75 ± 0.41 | 260.34 ± 0.63 | +23.59% | 63.89 ± 0.14 | 59.52 ± 0.12 | +7.34% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
