# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a1751c84f0d4`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2576.44 ± 17.20 | 3797.82 ± 26.01 | -32.16% | 164.21 ± 0.49 | 174.19 ± 0.28 | -5.73% |
| 256 | 4093.18 ± 7.38 | 4663.38 ± 28.49 | -12.23% | 163.92 ± 0.10 | 167.23 ± 0.55 | -1.98% |
| 512 | 5741.53 ± 24.06 | 5153.01 ± 5.96 | +11.42% | 162.95 ± 0.11 | 165.78 ± 0.92 | -1.71% |
| 1024 | 8137.96 ± 14.40 | 4613.36 ± 11.06 | +76.40% | 162.57 ± 0.28 | 164.59 ± 0.77 | -1.23% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
