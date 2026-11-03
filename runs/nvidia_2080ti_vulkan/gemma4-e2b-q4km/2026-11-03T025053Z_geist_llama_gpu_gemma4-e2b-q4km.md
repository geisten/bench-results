# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `c8df6888df6a`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2589.02 ± 4.41 | 3810.55 ± 12.67 | -32.06% | 158.69 ± 0.50 | 173.49 ± 0.40 | -8.53% |
| 256 | 4088.64 ± 9.00 | 4663.61 ± 6.07 | -12.33% | 158.49 ± 0.20 | 166.56 ± 0.54 | -4.85% |
| 512 | 5751.81 ± 23.92 | 5153.55 ± 8.28 | +11.61% | 157.67 ± 0.14 | 165.11 ± 0.47 | -4.50% |
| 1024 | 5584.92 ± 2.51 | 4620.44 ± 11.74 | +20.87% | 157.10 ± 0.11 | 163.75 ± 0.94 | -4.06% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
