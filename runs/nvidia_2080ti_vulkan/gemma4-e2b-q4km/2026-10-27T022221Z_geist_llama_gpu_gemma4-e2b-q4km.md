# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `df665fe9c736`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2573.93 ± 16.66 | 3809.48 ± 20.91 | -32.43% | 158.72 ± 0.74 | 173.24 ± 0.15 | -8.38% |
| 256 | 4074.75 ± 19.43 | 4667.18 ± 10.41 | -12.69% | 158.67 ± 0.39 | 166.08 ± 0.51 | -4.46% |
| 512 | 5736.99 ± 23.34 | 5149.81 ± 13.35 | +11.40% | 158.06 ± 0.23 | 164.98 ± 0.81 | -4.19% |
| 1024 | 5569.74 ± 17.09 | 4597.78 ± 5.62 | +21.14% | 157.50 ± 0.38 | 163.52 ± 0.46 | -3.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
