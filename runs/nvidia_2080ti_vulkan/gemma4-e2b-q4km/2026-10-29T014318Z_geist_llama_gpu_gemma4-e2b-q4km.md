# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `c212773b0268`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2568.22 ± 16.83 | 3784.97 ± 12.55 | -32.15% | 158.57 ± 0.22 | 173.44 ± 0.19 | -8.57% |
| 256 | 4088.00 ± 10.38 | 4651.76 ± 10.57 | -12.12% | 158.29 ± 0.07 | 165.97 ± 0.40 | -4.63% |
| 512 | 5748.52 ± 16.47 | 5137.61 ± 6.84 | +11.89% | 157.35 ± 0.02 | 164.73 ± 0.57 | -4.48% |
| 1024 | 5567.24 ± 15.41 | 4597.49 ± 3.46 | +21.09% | 156.85 ± 0.08 | 163.94 ± 0.55 | -4.32% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
