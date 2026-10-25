# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 24.50 ± 0.06 | 28.67 ± 0.29 | -14.54% | 5.85 ± 0.07 | 5.49 ± 0.03 | +6.49% |
| 256 | 24.11 ± 0.04 | 28.63 ± 0.14 | -15.78% | 5.63 ± 0.03 | 5.21 ± 0.06 | +8.00% |
| 512 | 23.13 ± 0.04 | 27.87 ± 0.08 | -16.99% | 5.29 ± 0.01 | 4.93 ± 0.04 | +7.29% |
| 1024 | 21.12 ± 0.01 | 26.75 ± 0.09 | -21.03% | 4.70 ± 0.01 | 4.09 ± 0.02 | +15.08% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
