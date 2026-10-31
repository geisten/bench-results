# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.09 ± 0.16 | 283.31 ± 0.53 | +27.45% | 70.17 ± 0.16 | 65.33 ± 0.27 | +7.42% |
| 256 | 357.34 ± 0.26 | 279.00 ± 1.36 | +28.08% | 68.46 ± 0.15 | 63.00 ± 0.13 | +8.66% |
| 512 | 340.80 ± 0.26 | 272.81 ± 1.26 | +24.93% | 65.34 ± 0.12 | 61.78 ± 0.09 | +5.77% |
| 1024 | 324.86 ± 0.17 | 257.13 ± 2.39 | +26.34% | 62.98 ± 0.06 | 59.65 ± 0.21 | +5.58% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
