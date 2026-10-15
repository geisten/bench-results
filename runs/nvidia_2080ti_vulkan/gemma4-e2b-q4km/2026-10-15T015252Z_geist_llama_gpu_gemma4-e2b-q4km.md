# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `ebcdfb017ba6`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2580.88 ± 7.41 | 3797.98 ± 9.78 | -32.05% | 158.39 ± 0.20 | 166.15 ± 0.47 | -4.67% |
| 256 | 4090.11 ± 6.37 | 4685.45 ± 19.94 | -12.71% | 158.84 ± 0.44 | 165.87 ± 0.48 | -4.24% |
| 512 | 5742.56 ± 30.31 | 5145.02 ± 13.26 | +11.61% | 157.89 ± 0.33 | 165.59 ± 0.47 | -4.65% |
| 1024 | 5571.26 ± 9.29 | 4605.70 ± 12.59 | +20.96% | 157.37 ± 0.30 | 164.73 ± 0.84 | -4.47% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
