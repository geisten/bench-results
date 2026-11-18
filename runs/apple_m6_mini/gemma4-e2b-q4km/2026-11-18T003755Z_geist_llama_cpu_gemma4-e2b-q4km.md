# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.79 ± 0.37 | 283.61 ± 0.04 | +27.21% | 72.39 ± 0.05 | 66.07 ± 0.06 | +9.57% |
| 256 | 353.95 ± 0.48 | 280.26 ± 0.19 | +26.29% | 70.21 ± 0.13 | 63.49 ± 0.07 | +10.59% |
| 512 | 340.53 ± 0.21 | 275.21 ± 0.39 | +23.73% | 66.56 ± 0.06 | 62.14 ± 0.08 | +7.11% |
| 1024 | 321.90 ± 0.21 | 260.98 ± 0.47 | +23.35% | 63.99 ± 0.04 | 60.17 ± 0.07 | +6.35% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
