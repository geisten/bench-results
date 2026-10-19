# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `2b5263f87833`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 190.51 ± 0.33 | 308.37 ± 0.58 | -38.22% | 50.74 ± 0.15 | 50.82 ± 0.18 | -0.16% |
| 256 | 186.08 ± 0.39 | 314.25 ± 1.82 | -40.78% | 46.49 ± 0.13 | 49.34 ± 0.15 | -5.77% |
| 512 | 172.30 ± 2.05 | 303.26 ± 3.54 | -43.19% | 40.18 ± 0.05 | 48.82 ± 0.16 | -17.70% |
| 1024 | 151.67 ± 2.49 | 292.53 ± 6.28 | -48.15% | 36.23 ± 0.18 | 47.69 ± 0.42 | -24.04% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
