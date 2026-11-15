# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 28.89 ± 0.25 | 29.96 ± 0.23 | -3.57% | 7.31 ± 0.28 | 6.58 ± 0.12 | +11.05% |
| 256 | 28.58 ± 0.09 | 29.56 ± 0.19 | -3.33% | 7.19 ± 0.18 | 6.41 ± 0.09 | +12.21% |
| 512 | 27.67 ± 0.05 | 28.43 ± 0.41 | -2.66% | 7.08 ± 0.10 | 6.34 ± 0.05 | +11.71% |
| 1024 | 26.60 ± 0.06 | 27.74 ± 0.26 | -4.10% | 6.96 ± 0.13 | 6.25 ± 0.05 | +11.44% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
