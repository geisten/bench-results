# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 29.17 ± 0.09 | 30.17 ± 0.47 | -3.33% | 7.37 ± 0.16 | 6.62 ± 0.06 | +11.42% |
| 256 | 28.72 ± 0.07 | 29.59 ± 0.15 | -2.94% | 7.21 ± 0.08 | 6.41 ± 0.05 | +12.57% |
| 512 | 27.80 ± 0.05 | 28.56 ± 0.24 | -2.64% | 7.05 ± 0.04 | 6.29 ± 0.04 | +12.09% |
| 1024 | 26.68 ± 0.03 | 28.13 ± 0.11 | -5.15% | 6.95 ± 0.05 | 6.25 ± 0.04 | +11.15% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
