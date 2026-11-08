# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.35 ± 0.25 | 283.62 ± 0.16 | +27.41% | 71.07 ± 0.06 | 65.30 ± 0.21 | +8.82% |
| 256 | 354.47 ± 0.62 | 280.15 ± 0.31 | +26.53% | 69.06 ± 0.09 | 62.83 ± 0.23 | +9.92% |
| 512 | 340.78 ± 0.30 | 275.19 ± 0.44 | +23.84% | 65.57 ± 0.11 | 61.30 ± 0.21 | +6.95% |
| 1024 | 322.41 ± 0.43 | 260.67 ± 0.65 | +23.69% | 63.06 ± 0.11 | 59.40 ± 0.21 | +6.16% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
