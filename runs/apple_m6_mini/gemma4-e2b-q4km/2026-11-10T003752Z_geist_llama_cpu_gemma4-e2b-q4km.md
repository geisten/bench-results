# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.34 ± 0.19 | 283.58 ± 0.13 | +27.42% | 71.22 ± 0.17 | 65.55 ± 0.30 | +8.66% |
| 256 | 354.45 ± 0.38 | 280.45 ± 0.25 | +26.39% | 69.15 ± 0.12 | 63.06 ± 0.29 | +9.67% |
| 512 | 341.09 ± 0.23 | 275.37 ± 0.48 | +23.87% | 65.70 ± 0.12 | 61.77 ± 0.38 | +6.36% |
| 1024 | 322.48 ± 0.31 | 261.00 ± 0.59 | +23.56% | 63.24 ± 0.13 | 59.78 ± 0.22 | +5.79% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
