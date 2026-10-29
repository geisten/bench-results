# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `1515c60147c9`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2615.21 ± 18.07 | 3719.61 ± 8.93 | -29.69% | 155.86 ± 0.26 | 191.51 ± 0.50 | -18.61% |
| 256 | 4064.72 ± 10.99 | 4176.07 ± 7.93 | -2.67% | 153.94 ± 0.06 | 184.21 ± 0.71 | -16.44% |
| 512 | 4884.50 ± 13.17 | 4722.42 ± 2.47 | +3.43% | 150.40 ± 0.09 | 181.96 ± 0.44 | -17.34% |
| 1024 | 4691.86 ± 4.58 | 4555.14 ± 6.34 | +3.00% | 148.66 ± 0.06 | 179.06 ± 0.72 | -16.97% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
