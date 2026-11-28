# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b0ee998e552`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5923.19 ± 35.29 | 3804.85 ± 11.90 | +55.67% | 164.37 ± 0.53 | 174.15 ± 0.25 | -5.62% |
| 256 | 9953.93 ± 28.91 | 4677.18 ± 13.47 | +112.82% | 163.62 ± 0.19 | 165.57 ± 0.65 | -1.18% |
| 512 | 14442.31 ± 61.33 | 5159.80 ± 11.32 | +179.90% | 163.14 ± 0.38 | 164.90 ± 0.55 | -1.07% |
| 1024 | 14721.85 ± 92.66 | 4605.91 ± 7.49 | +219.63% | 162.45 ± 0.18 | 163.08 ± 0.98 | -0.39% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
