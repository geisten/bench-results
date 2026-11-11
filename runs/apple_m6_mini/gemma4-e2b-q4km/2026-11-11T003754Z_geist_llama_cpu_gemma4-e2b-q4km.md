# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.07 ± 0.14 | 283.65 ± 0.16 | +27.29% | 71.35 ± 0.05 | 66.54 ± 0.19 | +7.23% |
| 256 | 356.91 ± 0.89 | 280.41 ± 0.12 | +27.28% | 69.30 ± 0.04 | 63.97 ± 0.15 | +8.33% |
| 512 | 340.62 ± 0.25 | 275.74 ± 0.41 | +23.53% | 65.77 ± 0.05 | 62.59 ± 0.10 | +5.08% |
| 1024 | 322.11 ± 0.31 | 261.14 ± 0.58 | +23.34% | 63.23 ± 0.09 | 60.58 ± 0.15 | +4.38% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
