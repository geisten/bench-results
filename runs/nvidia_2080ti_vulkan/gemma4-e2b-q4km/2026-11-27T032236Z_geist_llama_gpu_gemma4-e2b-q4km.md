# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5946.71 ± 24.14 | 3815.86 ± 5.06 | +55.84% | 165.10 ± 0.26 | 174.69 ± 0.26 | -5.49% |
| 256 | 9967.69 ± 68.77 | 4682.56 ± 16.10 | +112.87% | 164.31 ± 0.23 | 166.32 ± 0.90 | -1.21% |
| 512 | 14478.61 ± 99.77 | 5163.44 ± 9.76 | +180.41% | 163.38 ± 0.19 | 165.28 ± 0.45 | -1.16% |
| 1024 | 14762.99 ± 84.80 | 4609.27 ± 11.42 | +220.29% | 162.55 ± 0.46 | 163.21 ± 0.63 | -0.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
