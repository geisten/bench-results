# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `14ac9f78e1df`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2582.94 ± 10.73 | 3817.95 ± 6.07 | -32.35% | 159.09 ± 0.32 | 173.17 ± 0.35 | -8.13% |
| 256 | 4094.76 ± 5.31 | 4697.17 ± 9.71 | -12.83% | 159.56 ± 0.28 | 166.42 ± 0.65 | -4.12% |
| 512 | 5739.36 ± 21.12 | 5163.34 ± 15.89 | +11.16% | 158.39 ± 0.26 | 165.42 ± 0.70 | -4.25% |
| 1024 | 5576.23 ± 6.58 | 4624.33 ± 11.95 | +20.58% | 157.72 ± 0.35 | 163.97 ± 0.82 | -3.82% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
