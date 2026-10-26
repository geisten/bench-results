# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `eedaae6cae7b`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2573.12 ± 16.57 | 3767.44 ± 30.67 | -31.70% | 158.46 ± 0.44 | 173.24 ± 0.18 | -8.53% |
| 256 | 4085.24 ± 15.55 | 4665.66 ± 17.19 | -12.44% | 158.36 ± 0.11 | 166.39 ± 0.47 | -4.83% |
| 512 | 5747.95 ± 20.39 | 5142.59 ± 9.52 | +11.77% | 157.42 ± 0.06 | 165.41 ± 0.50 | -4.83% |
| 1024 | 5582.48 ± 5.22 | 4600.24 ± 9.50 | +21.35% | 156.95 ± 0.08 | 164.60 ± 0.81 | -4.65% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
