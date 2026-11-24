# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2589.44 ± 5.93 | 3810.18 ± 10.39 | -32.04% | 165.00 ± 0.34 | 174.55 ± 0.34 | -5.47% |
| 256 | 4107.02 ± 15.26 | 4673.45 ± 11.43 | -12.12% | 164.43 ± 0.51 | 166.10 ± 0.96 | -1.01% |
| 512 | 5760.09 ± 26.46 | 5142.91 ± 13.18 | +12.00% | 163.78 ± 0.32 | 164.62 ± 0.53 | -0.51% |
| 1024 | 8149.07 ± 16.40 | 4607.83 ± 9.02 | +76.85% | 162.63 ± 0.26 | 163.09 ± 0.89 | -0.28% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
