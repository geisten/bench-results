# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2627.21 ± 7.05 | 3738.29 ± 9.62 | -29.72% | 156.26 ± 0.35 | 192.63 ± 0.25 | -18.88% |
| 256 | 4076.18 ± 8.83 | 4175.39 ± 8.70 | -2.38% | 154.26 ± 0.29 | 183.84 ± 0.79 | -16.09% |
| 512 | 4884.61 ± 13.43 | 4729.60 ± 5.04 | +3.28% | 151.01 ± 0.18 | 181.12 ± 0.45 | -16.63% |
| 1024 | 4686.46 ± 8.49 | 4565.03 ± 4.77 | +2.66% | 149.01 ± 0.19 | 178.23 ± 0.55 | -16.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
