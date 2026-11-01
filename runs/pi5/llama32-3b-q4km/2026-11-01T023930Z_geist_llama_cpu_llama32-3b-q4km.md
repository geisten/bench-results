# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 24.61 ± 0.09 | 28.44 ± 0.31 | -13.47% | 5.82 ± 0.07 | 5.35 ± 0.02 | +8.82% |
| 256 | 24.14 ± 0.04 | 28.35 ± 0.17 | -14.84% | 5.63 ± 0.01 | 5.15 ± 0.01 | +9.32% |
| 512 | 23.19 ± 0.06 | 27.59 ± 0.15 | -15.95% | 5.29 ± 0.01 | 4.90 ± 0.03 | +8.05% |
| 1024 | 21.15 ± 0.05 | 26.28 ± 0.25 | -19.53% | 4.70 ± 0.01 | 4.03 ± 0.01 | +16.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
