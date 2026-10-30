# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `448c3d120a97`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.56 ± 0.32 | 283.32 ± 0.47 | +27.26% | 71.94 ± 0.04 | 66.65 ± 0.06 | +7.93% |
| 256 | 357.00 ± 0.21 | 278.06 ± 1.49 | +28.39% | 69.81 ± 0.10 | 64.09 ± 0.05 | +8.93% |
| 512 | 340.76 ± 0.32 | 272.34 ± 1.33 | +25.13% | 66.28 ± 0.07 | 62.65 ± 0.09 | +5.80% |
| 1024 | 324.24 ± 0.52 | 256.28 ± 1.67 | +26.52% | 63.72 ± 0.07 | 60.70 ± 0.04 | +4.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
