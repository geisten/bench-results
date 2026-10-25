# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 28.99 ± 0.10 | 30.04 ± 0.43 | -3.50% | 7.51 ± 0.03 | 6.49 ± 0.10 | +15.73% |
| 256 | 28.52 ± 0.09 | 29.86 ± 0.35 | -4.48% | 7.25 ± 0.05 | 6.36 ± 0.09 | +14.07% |
| 512 | 27.62 ± 0.05 | 29.04 ± 0.08 | -4.88% | 7.09 ± 0.08 | 6.26 ± 0.07 | +13.37% |
| 1024 | 26.54 ± 0.08 | 28.38 ± 0.06 | -6.52% | 7.03 ± 0.02 | 6.18 ± 0.09 | +13.85% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
