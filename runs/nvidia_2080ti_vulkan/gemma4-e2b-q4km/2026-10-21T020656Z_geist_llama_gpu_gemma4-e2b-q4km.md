# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `5afe43c5b436`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2576.65 ± 17.12 | 3813.60 ± 10.94 | -32.44% | 158.42 ± 0.58 | 173.09 ± 0.19 | -8.47% |
| 256 | 4079.26 ± 9.77 | 4681.80 ± 15.58 | -12.87% | 159.12 ± 0.11 | 166.18 ± 0.52 | -4.25% |
| 512 | 5726.79 ± 17.50 | 5146.26 ± 14.91 | +11.28% | 157.68 ± 0.24 | 165.01 ± 0.36 | -4.44% |
| 1024 | 5567.78 ± 7.09 | 4609.67 ± 17.67 | +20.78% | 157.47 ± 0.31 | 164.18 ± 0.64 | -4.09% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
