# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2580.91 ± 15.12 | 3806.39 ± 11.93 | -32.20% | 164.85 ± 0.33 | 174.09 ± 0.31 | -5.31% |
| 256 | 4091.85 ± 14.21 | 4668.05 ± 16.64 | -12.34% | 163.77 ± 0.22 | 167.02 ± 0.47 | -1.95% |
| 512 | 5761.68 ± 8.41 | 5142.31 ± 11.23 | +12.04% | 162.84 ± 0.06 | 165.61 ± 0.27 | -1.68% |
| 1024 | 5571.74 ± 13.20 | 4603.46 ± 14.09 | +21.03% | 162.26 ± 0.05 | 163.84 ± 0.80 | -0.96% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
