# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `527bf29dd426`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2579.31 ± 9.85 | 3737.88 ± 80.83 | -31.00% | 158.41 ± 0.28 | 166.19 ± 0.63 | -4.68% |
| 256 | 4100.54 ± 10.33 | 4671.90 ± 10.71 | -12.23% | 158.90 ± 0.07 | 166.07 ± 0.30 | -4.32% |
| 512 | 5733.62 ± 31.38 | 5151.52 ± 8.17 | +11.30% | 157.98 ± 0.49 | 165.39 ± 0.70 | -4.48% |
| 1024 | 5572.24 ± 14.77 | 4610.65 ± 14.92 | +20.86% | 157.69 ± 0.26 | 164.75 ± 0.72 | -4.28% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
