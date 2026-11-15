# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 24.53 ± 0.08 | 28.43 ± 0.12 | -13.70% | 5.39 ± 0.07 | 5.29 ± 0.06 | +1.95% |
| 256 | 24.08 ± 0.06 | 28.25 ± 0.15 | -14.76% | 5.22 ± 0.02 | 5.04 ± 0.10 | +3.43% |
| 512 | 23.18 ± 0.04 | 27.50 ± 0.05 | -15.71% | 4.93 ± 0.01 | 4.79 ± 0.09 | +2.91% |
| 1024 | 21.22 ± 0.02 | 26.40 ± 0.13 | -19.64% | 4.43 ± 0.01 | 3.96 ± 0.03 | +11.93% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
