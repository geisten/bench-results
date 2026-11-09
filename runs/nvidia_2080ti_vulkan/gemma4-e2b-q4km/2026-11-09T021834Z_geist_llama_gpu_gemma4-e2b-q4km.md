# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2585.12 ± 10.63 | 3806.96 ± 9.78 | -32.09% | 158.59 ± 0.54 | 173.41 ± 0.16 | -8.55% |
| 256 | 4096.56 ± 5.28 | 4660.95 ± 20.62 | -12.11% | 158.39 ± 0.37 | 166.74 ± 0.79 | -5.01% |
| 512 | 5748.85 ± 22.31 | 5145.49 ± 16.16 | +11.73% | 157.15 ± 0.07 | 165.07 ± 0.54 | -4.80% |
| 1024 | 5574.41 ± 11.42 | 4610.72 ± 14.72 | +20.90% | 156.63 ± 0.05 | 164.24 ± 0.39 | -4.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
