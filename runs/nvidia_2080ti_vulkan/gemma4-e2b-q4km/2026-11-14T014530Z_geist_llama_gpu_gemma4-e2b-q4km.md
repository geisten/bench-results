# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2569.75 ± 19.98 | 3806.01 ± 7.45 | -32.48% | 163.19 ± 0.22 | 173.36 ± 0.15 | -5.87% |
| 256 | 4087.83 ± 9.43 | 4657.89 ± 15.40 | -12.24% | 162.71 ± 0.07 | 166.50 ± 0.40 | -2.28% |
| 512 | 5758.38 ± 23.05 | 5152.89 ± 8.18 | +11.75% | 161.81 ± 0.07 | 165.27 ± 0.54 | -2.09% |
| 1024 | 5578.51 ± 10.33 | 4619.33 ± 6.23 | +20.76% | 161.72 ± 0.29 | 164.38 ± 0.94 | -1.62% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
