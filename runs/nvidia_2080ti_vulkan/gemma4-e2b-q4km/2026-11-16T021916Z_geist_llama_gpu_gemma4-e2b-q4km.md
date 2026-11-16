# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2577.76 ± 8.70 | 3797.94 ± 9.45 | -32.13% | 164.26 ± 0.18 | 173.93 ± 0.18 | -5.56% |
| 256 | 4091.45 ± 6.48 | 4665.89 ± 12.01 | -12.31% | 163.68 ± 0.11 | 166.04 ± 0.82 | -1.42% |
| 512 | 5764.44 ± 13.73 | 5148.53 ± 8.42 | +11.96% | 162.83 ± 0.17 | 165.19 ± 0.64 | -1.43% |
| 1024 | 5590.51 ± 10.15 | 4595.40 ± 12.39 | +21.65% | 162.46 ± 0.32 | 164.59 ± 0.75 | -1.30% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
