# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 28.91 ± 0.18 | 29.91 ± 0.33 | -3.34% | 7.43 ± 0.07 | 6.72 ± 0.06 | +10.61% |
| 256 | 28.49 ± 0.06 | 29.65 ± 0.29 | -3.89% | 7.30 ± 0.02 | 6.49 ± 0.04 | +12.40% |
| 512 | 27.62 ± 0.05 | 28.68 ± 0.12 | -3.68% | 7.11 ± 0.08 | 6.44 ± 0.02 | +10.39% |
| 1024 | 26.52 ± 0.08 | 27.71 ± 0.08 | -4.29% | 7.04 ± 0.03 | 6.29 ± 0.06 | +11.83% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
