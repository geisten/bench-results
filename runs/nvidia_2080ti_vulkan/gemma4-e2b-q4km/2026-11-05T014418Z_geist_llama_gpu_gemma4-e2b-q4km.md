# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `406a3c0519ec`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2574.91 ± 10.55 | 3784.40 ± 18.84 | -31.96% | 158.20 ± 0.34 | 173.35 ± 0.55 | -8.74% |
| 256 | 4084.55 ± 16.44 | 4661.87 ± 17.03 | -12.38% | 158.14 ± 0.20 | 166.42 ± 0.56 | -4.98% |
| 512 | 5747.68 ± 25.39 | 5139.39 ± 16.44 | +11.84% | 157.20 ± 0.40 | 164.74 ± 0.87 | -4.57% |
| 1024 | 5571.61 ± 8.00 | 4603.93 ± 10.29 | +21.02% | 156.58 ± 0.15 | 163.56 ± 0.36 | -4.26% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
