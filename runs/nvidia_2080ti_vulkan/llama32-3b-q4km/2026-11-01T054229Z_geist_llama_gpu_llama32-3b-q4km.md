# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2618.26 ± 9.73 | 3769.90 ± 9.25 | -30.55% | 156.25 ± 0.35 | 193.87 ± 0.20 | -19.40% |
| 256 | 4069.11 ± 6.95 | 4184.27 ± 20.41 | -2.75% | 154.50 ± 0.31 | 184.09 ± 0.46 | -16.07% |
| 512 | 4876.73 ± 16.48 | 4737.59 ± 10.66 | +2.94% | 150.88 ± 0.20 | 181.68 ± 0.35 | -16.95% |
| 1024 | 4680.42 ± 4.16 | 4574.39 ± 8.99 | +2.32% | 149.11 ± 0.20 | 178.37 ± 0.50 | -16.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
