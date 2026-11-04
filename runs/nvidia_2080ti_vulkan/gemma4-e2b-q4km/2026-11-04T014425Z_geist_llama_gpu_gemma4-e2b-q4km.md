# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2570.05 ± 13.30 | 3800.65 ± 8.63 | -32.38% | 158.57 ± 0.28 | 173.46 ± 0.39 | -8.59% |
| 256 | 4087.15 ± 15.78 | 4650.82 ± 9.20 | -12.12% | 158.83 ± 0.41 | 166.52 ± 0.83 | -4.62% |
| 512 | 5741.33 ± 17.58 | 5140.06 ± 12.51 | +11.70% | 157.69 ± 0.18 | 165.22 ± 0.79 | -4.56% |
| 1024 | 5571.50 ± 6.59 | 4601.59 ± 11.18 | +21.08% | 156.92 ± 0.17 | 164.19 ± 0.43 | -4.43% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
