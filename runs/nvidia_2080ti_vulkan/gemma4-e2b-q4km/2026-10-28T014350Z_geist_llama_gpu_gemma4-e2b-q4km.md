# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `13921becb240`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2580.08 ± 9.27 | 3807.24 ± 7.91 | -32.23% | 158.91 ± 0.25 | 173.58 ± 0.27 | -8.45% |
| 256 | 4096.72 ± 13.18 | 4660.19 ± 13.44 | -12.09% | 158.75 ± 0.37 | 166.21 ± 0.79 | -4.49% |
| 512 | 5720.54 ± 25.62 | 5132.87 ± 10.85 | +11.45% | 157.39 ± 0.11 | 164.98 ± 0.30 | -4.60% |
| 1024 | 5564.66 ± 12.86 | 4577.26 ± 5.78 | +21.57% | 156.93 ± 0.42 | 163.87 ± 1.13 | -4.24% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
