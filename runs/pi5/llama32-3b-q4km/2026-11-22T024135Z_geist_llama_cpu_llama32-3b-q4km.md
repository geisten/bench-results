# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 24.59 ± 0.07 | 28.16 ± 0.28 | -12.70% | 5.41 ± 0.06 | 5.31 ± 0.06 | +1.93% |
| 256 | 24.17 ± 0.05 | 28.11 ± 0.20 | -14.00% | 5.21 ± 0.03 | 5.08 ± 0.04 | +2.64% |
| 512 | 23.31 ± 0.01 | 27.30 ± 0.11 | -14.63% | 4.92 ± 0.02 | 4.85 ± 0.05 | +1.54% |
| 1024 | 21.31 ± 0.03 | 26.13 ± 0.18 | -18.45% | 4.43 ± 0.02 | 4.03 ± 0.04 | +9.80% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
