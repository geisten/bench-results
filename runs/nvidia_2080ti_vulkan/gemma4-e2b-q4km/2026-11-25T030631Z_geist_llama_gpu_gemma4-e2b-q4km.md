# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2591.36 ± 3.10 | 3811.48 ± 9.88 | -32.01% | 164.72 ± 0.11 | 174.93 ± 0.13 | -5.83% |
| 256 | 4117.01 ± 3.94 | 4684.39 ± 19.95 | -12.11% | 164.46 ± 0.08 | 167.48 ± 0.85 | -1.81% |
| 512 | 5769.47 ± 24.55 | 5163.08 ± 9.92 | +11.74% | 162.99 ± 0.21 | 165.08 ± 0.68 | -1.27% |
| 1024 | 8148.23 ± 19.28 | 4620.64 ± 17.61 | +76.34% | 162.47 ± 0.19 | 163.44 ± 0.42 | -0.59% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
