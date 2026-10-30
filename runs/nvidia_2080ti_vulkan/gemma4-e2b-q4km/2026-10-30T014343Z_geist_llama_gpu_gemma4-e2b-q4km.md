# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2567.96 ± 14.67 | 3810.88 ± 14.71 | -32.61% | 158.79 ± 0.77 | 173.39 ± 0.35 | -8.42% |
| 256 | 4087.60 ± 15.03 | 4659.12 ± 8.97 | -12.27% | 159.01 ± 0.46 | 165.87 ± 0.38 | -4.13% |
| 512 | 5744.50 ± 18.35 | 5124.25 ± 4.89 | +12.10% | 157.81 ± 0.20 | 165.09 ± 0.48 | -4.41% |
| 1024 | 5570.35 ± 10.56 | 4591.36 ± 10.12 | +21.32% | 157.15 ± 0.06 | 163.68 ± 0.17 | -3.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
