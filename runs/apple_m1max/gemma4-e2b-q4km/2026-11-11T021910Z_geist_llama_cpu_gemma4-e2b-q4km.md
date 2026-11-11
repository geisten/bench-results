# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 350.79 ± 0.72 | 308.12 ± 1.40 | +13.85% | 63.16 ± 0.24 | 51.03 ± 0.17 | +23.76% |
| 256 | 344.61 ± 1.40 | 308.62 ± 4.99 | +11.66% | 60.96 ± 0.17 | 49.46 ± 0.16 | +23.25% |
| 512 | 327.46 ± 2.66 | 298.88 ± 8.88 | +9.56% | 57.04 ± 0.25 | 48.60 ± 0.11 | +17.38% |
| 1024 | 297.23 ± 5.85 | 285.19 ± 9.85 | +4.22% | 54.07 ± 0.38 | 47.49 ± 0.38 | +13.86% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
