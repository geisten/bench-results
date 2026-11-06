# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2568.09 ± 23.95 | 3797.15 ± 6.24 | -32.37% | 158.03 ± 0.63 | 173.24 ± 0.35 | -8.78% |
| 256 | 4087.45 ± 10.39 | 4664.48 ± 7.71 | -12.37% | 157.97 ± 0.10 | 166.20 ± 0.74 | -4.95% |
| 512 | 5746.81 ± 20.42 | 5145.73 ± 3.79 | +11.68% | 157.05 ± 0.10 | 165.59 ± 0.35 | -5.16% |
| 1024 | 5573.44 ± 10.65 | 4602.08 ± 3.29 | +21.11% | 156.59 ± 0.05 | 163.92 ± 0.57 | -4.47% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
