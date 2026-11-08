# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 28.93 ± 0.12 | 30.03 ± 0.29 | -3.67% | 7.40 ± 0.14 | 6.68 ± 0.07 | +10.72% |
| 256 | 28.55 ± 0.08 | 30.02 ± 0.27 | -4.89% | 7.26 ± 0.06 | 6.48 ± 0.08 | +12.14% |
| 512 | 27.66 ± 0.05 | 28.96 ± 0.12 | -4.48% | 7.10 ± 0.04 | 6.37 ± 0.07 | +11.48% |
| 1024 | 26.60 ± 0.04 | 28.13 ± 0.22 | -5.46% | 7.03 ± 0.02 | 6.29 ± 0.07 | +11.66% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
