# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 29.01 ± 0.06 | 30.02 ± 0.41 | -3.36% | 7.51 ± 0.02 | 6.58 ± 0.08 | +14.24% |
| 256 | 28.64 ± 0.04 | 29.95 ± 0.16 | -4.39% | 7.31 ± 0.06 | 6.47 ± 0.08 | +13.01% |
| 512 | 27.74 ± 0.03 | 28.87 ± 0.18 | -3.90% | 7.10 ± 0.01 | 6.30 ± 0.07 | +12.81% |
| 1024 | 26.57 ± 0.02 | 28.31 ± 0.11 | -6.16% | 6.97 ± 0.01 | 6.30 ± 0.07 | +10.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
