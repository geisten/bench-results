# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 493.58 ± 9.23 | 450.80 ± 0.29 | +9.49% | 36.82 ± 0.03 | 35.09 ± 0.04 | +4.92% |
| 256 | 495.90 ± 26.45 | 454.76 ± 0.97 | +9.05% | 36.63 ± 0.04 | 34.60 ± 0.04 | +5.86% |
| 512 | 505.41 ± 22.11 | 454.94 ± 0.64 | +11.09% | 36.30 ± 0.23 | 33.98 ± 0.04 | +6.83% |
| 1024 | 484.80 ± 20.34 | 442.22 ± 0.97 | +9.63% | 35.69 ± 0.43 | 32.79 ± 0.07 | +8.84% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
