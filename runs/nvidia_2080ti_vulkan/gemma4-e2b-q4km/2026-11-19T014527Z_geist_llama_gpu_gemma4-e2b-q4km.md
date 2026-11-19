# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2583.03 ± 14.51 | 3802.12 ± 17.61 | -32.06% | 164.75 ± 0.44 | 174.18 ± 0.18 | -5.41% |
| 256 | 4097.41 ± 7.59 | 4659.71 ± 17.92 | -12.07% | 164.04 ± 0.32 | 166.45 ± 0.77 | -1.45% |
| 512 | 5754.23 ± 23.79 | 5143.89 ± 9.99 | +11.87% | 162.85 ± 0.21 | 164.30 ± 0.28 | -0.88% |
| 1024 | 5569.67 ± 18.23 | 4600.59 ± 12.86 | +21.06% | 162.29 ± 0.05 | 163.90 ± 0.98 | -0.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
