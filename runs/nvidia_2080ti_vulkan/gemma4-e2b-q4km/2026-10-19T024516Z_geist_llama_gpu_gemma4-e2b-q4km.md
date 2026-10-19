# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `2b5263f87833`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2573.51 ± 13.28 | 3816.95 ± 13.13 | -32.58% | 158.40 ± 0.64 | 173.57 ± 0.35 | -8.74% |
| 256 | 4105.59 ± 6.91 | 4687.98 ± 12.34 | -12.42% | 159.35 ± 0.33 | 166.48 ± 0.52 | -4.28% |
| 512 | 5753.46 ± 16.44 | 5153.89 ± 15.53 | +11.63% | 158.41 ± 0.18 | 165.63 ± 0.22 | -4.36% |
| 1024 | 5578.16 ± 10.46 | 4618.94 ± 9.51 | +20.77% | 157.81 ± 0.18 | 163.79 ± 0.74 | -3.65% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
