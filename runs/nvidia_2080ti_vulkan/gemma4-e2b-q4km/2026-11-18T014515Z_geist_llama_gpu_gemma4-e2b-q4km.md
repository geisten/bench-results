# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2574.18 ± 13.98 | 3690.43 ± 120.92 | -30.25% | 164.26 ± 0.36 | 174.30 ± 0.43 | -5.76% |
| 256 | 4092.73 ± 10.89 | 4663.51 ± 7.33 | -12.24% | 163.97 ± 0.19 | 165.99 ± 0.46 | -1.22% |
| 512 | 5774.79 ± 21.03 | 5144.15 ± 17.73 | +12.26% | 163.08 ± 0.34 | 164.94 ± 0.63 | -1.13% |
| 1024 | 5577.36 ± 7.56 | 4594.58 ± 13.66 | +21.39% | 162.23 ± 0.02 | 163.84 ± 0.86 | -0.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
