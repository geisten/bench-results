# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2582.82 ± 8.06 | 3790.27 ± 13.19 | -31.86% | 163.85 ± 0.25 | 173.49 ± 0.31 | -5.56% |
| 256 | 4097.84 ± 5.37 | 4660.78 ± 19.20 | -12.08% | 163.09 ± 0.25 | 167.09 ± 0.65 | -2.39% |
| 512 | 5757.21 ± 13.82 | 5139.34 ± 5.41 | +12.02% | 161.89 ± 0.08 | 165.01 ± 0.27 | -1.89% |
| 1024 | 5581.29 ± 9.60 | 4607.48 ± 12.60 | +21.14% | 161.31 ± 0.20 | 164.04 ± 0.94 | -1.67% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
