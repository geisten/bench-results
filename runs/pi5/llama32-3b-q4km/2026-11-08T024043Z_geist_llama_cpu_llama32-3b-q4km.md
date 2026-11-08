# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 24.53 ± 0.04 | 28.27 ± 0.27 | -13.23% | 5.35 ± 0.05 | 5.36 ± 0.03 | -0.29% |
| 256 | 24.09 ± 0.03 | 28.33 ± 0.12 | -14.95% | 5.17 ± 0.02 | 5.19 ± 0.03 | -0.26% |
| 512 | 23.22 ± 0.03 | 27.61 ± 0.12 | -15.87% | 4.89 ± 0.01 | 4.98 ± 0.03 | -1.82% |
| 1024 | 21.24 ± 0.02 | 26.43 ± 0.22 | -19.64% | 4.39 ± 0.01 | 4.07 ± 0.03 | +8.01% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
