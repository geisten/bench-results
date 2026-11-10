# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2576.41 ± 16.62 | 3795.55 ± 19.44 | -32.12% | 158.29 ± 0.33 | 173.21 ± 0.33 | -8.62% |
| 256 | 4084.98 ± 18.21 | 4667.03 ± 23.31 | -12.47% | 158.58 ± 0.51 | 166.14 ± 0.58 | -4.55% |
| 512 | 5740.06 ± 33.35 | 5145.79 ± 8.39 | +11.55% | 157.61 ± 0.10 | 164.94 ± 0.31 | -4.44% |
| 1024 | 5588.88 ± 4.95 | 4602.60 ± 9.32 | +21.43% | 157.22 ± 0.50 | 164.07 ± 0.51 | -4.18% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
