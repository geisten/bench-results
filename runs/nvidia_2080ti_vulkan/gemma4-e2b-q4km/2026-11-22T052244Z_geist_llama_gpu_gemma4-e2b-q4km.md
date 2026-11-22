# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2570.88 ± 6.08 | 3816.31 ± 9.12 | -32.63% | 164.47 ± 0.22 | 174.44 ± 0.29 | -5.71% |
| 256 | 4094.30 ± 6.26 | 4688.50 ± 13.24 | -12.67% | 164.05 ± 0.24 | 165.75 ± 0.42 | -1.03% |
| 512 | 5763.88 ± 14.34 | 5164.13 ± 20.11 | +11.61% | 163.01 ± 0.21 | 164.47 ± 0.73 | -0.88% |
| 1024 | 5599.21 ± 9.63 | 4631.27 ± 9.59 | +20.90% | 162.56 ± 0.04 | 164.64 ± 0.81 | -1.26% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
