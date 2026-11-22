# Current CPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 719.75 ± 16.16 | 490.53 ± 1.77 | +46.73% | 37.16 ± 0.15 | 35.89 ± 0.03 | +3.55% |
| 256 | 736.13 ± 2.80 | 504.43 ± 2.08 | +45.93% | 37.06 ± 0.10 | 35.26 ± 0.03 | +5.09% |
| 512 | 722.01 ± 4.40 | 511.62 ± 0.91 | +41.12% | 36.81 ± 0.09 | 34.67 ± 0.08 | +6.16% |
| 1024 | 695.24 ± 4.95 | 494.81 ± 2.38 | +40.51% | 36.14 ± 0.07 | 33.46 ± 0.09 | +8.01% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
