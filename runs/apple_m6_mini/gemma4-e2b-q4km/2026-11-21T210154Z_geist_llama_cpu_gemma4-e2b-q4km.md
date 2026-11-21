# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.72 ± 0.20 | 283.67 ± 0.05 | +27.16% | 72.16 ± 0.10 | 66.37 ± 0.07 | +8.73% |
| 256 | 355.28 ± 1.79 | 280.52 ± 0.17 | +26.65% | 70.06 ± 0.08 | 63.80 ± 0.06 | +9.82% |
| 512 | 340.20 ± 0.33 | 274.90 ± 0.39 | +23.75% | 66.43 ± 0.08 | 62.46 ± 0.02 | +6.36% |
| 1024 | 321.64 ± 0.22 | 261.10 ± 0.45 | +23.19% | 63.91 ± 0.05 | 60.48 ± 0.05 | +5.67% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
