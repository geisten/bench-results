# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2570.75 ± 7.53 | 3804.26 ± 13.12 | -32.42% | 164.07 ± 0.34 | 173.93 ± 0.25 | -5.67% |
| 256 | 4088.05 ± 12.89 | 4667.68 ± 10.84 | -12.42% | 163.54 ± 0.40 | 165.64 ± 0.74 | -1.27% |
| 512 | 5753.59 ± 16.47 | 5153.32 ± 8.19 | +11.65% | 163.03 ± 0.41 | 164.94 ± 1.08 | -1.16% |
| 1024 | 5581.17 ± 11.25 | 4601.89 ± 11.19 | +21.28% | 162.26 ± 0.17 | 164.20 ± 1.24 | -1.18% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
