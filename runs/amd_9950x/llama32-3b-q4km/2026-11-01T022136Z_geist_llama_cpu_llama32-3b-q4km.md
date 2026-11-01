# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 740.46 ± 1.22 | 502.90 ± 3.09 | +47.24% | 37.55 ± 0.07 | 35.63 ± 0.06 | +5.39% |
| 256 | 746.28 ± 1.16 | 515.52 ± 2.74 | +44.76% | 37.52 ± 0.08 | 35.15 ± 0.04 | +6.73% |
| 512 | 735.36 ± 5.24 | 519.21 ± 2.44 | +41.63% | 37.20 ± 0.09 | 34.56 ± 0.07 | +7.62% |
| 1024 | 708.73 ± 2.45 | 503.56 ± 1.71 | +40.74% | 36.56 ± 0.04 | 33.33 ± 0.07 | +9.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
