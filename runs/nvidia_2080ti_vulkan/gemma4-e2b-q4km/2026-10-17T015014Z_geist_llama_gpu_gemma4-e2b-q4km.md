# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b892b0f366c`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2568.43 ± 22.59 | 3800.07 ± 13.32 | -32.41% | 158.18 ± 1.02 | 173.38 ± 0.18 | -8.77% |
| 256 | 4087.47 ± 17.06 | 4679.97 ± 21.42 | -12.66% | 159.24 ± 0.47 | 166.24 ± 0.77 | -4.21% |
| 512 | 5736.12 ± 18.38 | 5142.50 ± 8.23 | +11.54% | 158.07 ± 0.34 | 164.93 ± 0.52 | -4.16% |
| 1024 | 5577.42 ± 6.93 | 4609.48 ± 10.30 | +21.00% | 157.86 ± 0.26 | 163.95 ± 0.48 | -3.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
