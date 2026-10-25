# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 344.61 ± 1.54 | 304.70 ± 4.07 | +13.10% | 62.26 ± 0.27 | 50.92 ± 0.42 | +22.26% |
| 256 | 337.40 ± 2.17 | 298.91 ± 11.08 | +12.88% | 59.77 ± 0.43 | 49.66 ± 0.17 | +20.37% |
| 512 | 325.43 ± 2.48 | 301.66 ± 8.01 | +7.88% | 56.02 ± 0.25 | 48.49 ± 0.39 | +15.53% |
| 1024 | 303.02 ± 3.56 | 282.80 ± 6.16 | +7.15% | 53.73 ± 0.15 | 47.26 ± 0.68 | +13.68% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
