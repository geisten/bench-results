# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `fda9c7a98c7b`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2579.22 ± 9.70 | 3628.30 ± 183.92 | -28.91% | 158.12 ± 0.46 | 166.31 ± 0.99 | -4.92% |
| 256 | 4091.81 ± 9.11 | 4666.83 ± 22.61 | -12.32% | 158.64 ± 0.14 | 166.46 ± 0.40 | -4.70% |
| 512 | 5745.42 ± 25.71 | 5144.02 ± 3.14 | +11.69% | 157.94 ± 0.06 | 164.91 ± 0.66 | -4.23% |
| 1024 | 5568.11 ± 14.13 | 4606.51 ± 16.14 | +20.87% | 157.20 ± 0.27 | 164.54 ± 0.41 | -4.46% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
