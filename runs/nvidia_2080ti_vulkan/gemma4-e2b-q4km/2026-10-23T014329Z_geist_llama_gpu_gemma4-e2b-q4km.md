# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `cdc4ba43c58a`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2569.95 ± 7.27 | 3799.18 ± 10.19 | -32.36% | 158.42 ± 0.26 | 173.23 ± 0.32 | -8.55% |
| 256 | 4089.10 ± 8.20 | 4654.79 ± 8.13 | -12.15% | 158.30 ± 0.09 | 165.96 ± 0.39 | -4.61% |
| 512 | 5723.36 ± 23.06 | 5129.35 ± 12.25 | +11.58% | 157.20 ± 0.08 | 164.60 ± 0.46 | -4.49% |
| 1024 | 5560.43 ± 9.73 | 4594.64 ± 10.24 | +21.02% | 156.71 ± 0.15 | 163.41 ± 0.56 | -4.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
