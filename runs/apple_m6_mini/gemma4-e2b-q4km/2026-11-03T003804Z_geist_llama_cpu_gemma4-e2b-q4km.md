# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.20 ± 0.13 | 283.90 ± 0.13 | +27.23% | 71.45 ± 0.06 | 66.70 ± 0.03 | +7.12% |
| 256 | 357.50 ± 0.21 | 280.64 ± 0.10 | +27.38% | 69.34 ± 0.03 | 64.06 ± 0.11 | +8.25% |
| 512 | 340.85 ± 0.48 | 275.38 ± 0.61 | +23.78% | 65.79 ± 0.10 | 62.78 ± 0.04 | +4.80% |
| 1024 | 325.07 ± 0.15 | 260.96 ± 0.77 | +24.57% | 63.24 ± 0.08 | 60.69 ± 0.03 | +4.20% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
