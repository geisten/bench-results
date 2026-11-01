# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2570.88 ± 19.32 | 3815.16 ± 5.50 | -32.61% | 159.25 ± 0.18 | 173.55 ± 0.27 | -8.24% |
| 256 | 4073.78 ± 22.55 | 4675.02 ± 13.71 | -12.86% | 158.52 ± 0.17 | 166.52 ± 0.50 | -4.81% |
| 512 | 5742.26 ± 24.66 | 5145.02 ± 9.07 | +11.61% | 158.26 ± 0.17 | 165.44 ± 0.67 | -4.34% |
| 1024 | 5582.97 ± 11.48 | 4602.60 ± 7.29 | +21.30% | 157.79 ± 0.12 | 163.73 ± 0.77 | -3.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
