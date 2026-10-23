# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f19377734f16`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2569.64 ± 23.05 | 3800.73 ± 6.38 | -32.39% | 158.29 ± 0.98 | 173.16 ± 0.19 | -8.58% |
| 256 | 4083.14 ± 12.63 | 4656.47 ± 7.89 | -12.31% | 158.70 ± 0.29 | 166.04 ± 0.39 | -4.42% |
| 512 | 5735.93 ± 17.20 | 5138.59 ± 12.01 | +11.62% | 157.53 ± 0.10 | 164.32 ± 0.45 | -4.13% |
| 1024 | 5558.99 ± 14.74 | 4597.21 ± 6.64 | +20.92% | 157.04 ± 0.10 | 163.67 ± 0.92 | -4.05% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
