# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.85 ± 0.16 | 283.52 ± 0.06 | +27.28% | 72.19 ± 0.04 | 65.69 ± 0.17 | +9.90% |
| 256 | 353.84 ± 0.22 | 280.16 ± 0.18 | +26.30% | 70.08 ± 0.05 | 63.17 ± 0.16 | +10.93% |
| 512 | 340.46 ± 0.26 | 274.96 ± 1.02 | +23.82% | 66.47 ± 0.04 | 61.85 ± 0.15 | +7.46% |
| 1024 | 321.57 ± 0.21 | 260.38 ± 0.47 | +23.50% | 63.86 ± 0.08 | 59.91 ± 0.11 | +6.60% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
