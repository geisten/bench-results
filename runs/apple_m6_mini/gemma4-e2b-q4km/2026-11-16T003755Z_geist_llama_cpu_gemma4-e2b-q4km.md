# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.80 ± 0.16 | 283.87 ± 0.08 | +27.10% | 69.90 ± 0.08 | 66.36 ± 0.06 | +5.34% |
| 256 | 353.73 ± 0.19 | 280.34 ± 0.13 | +26.18% | 67.88 ± 0.11 | 63.77 ± 0.04 | +6.45% |
| 512 | 340.22 ± 0.41 | 275.83 ± 0.35 | +23.34% | 64.49 ± 0.06 | 62.38 ± 0.04 | +3.39% |
| 1024 | 322.15 ± 0.39 | 260.93 ± 0.56 | +23.46% | 62.12 ± 0.04 | 60.42 ± 0.06 | +2.82% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
