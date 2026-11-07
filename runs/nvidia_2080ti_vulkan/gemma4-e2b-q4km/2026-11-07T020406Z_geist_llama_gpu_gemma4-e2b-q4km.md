# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2571.08 ± 16.95 | 3817.10 ± 7.47 | -32.64% | 158.58 ± 0.34 | 173.42 ± 0.45 | -8.56% |
| 256 | 4088.55 ± 15.99 | 4675.34 ± 10.12 | -12.55% | 158.38 ± 0.17 | 166.83 ± 0.59 | -5.07% |
| 512 | 5746.93 ± 14.33 | 5148.41 ± 5.76 | +11.63% | 157.60 ± 0.25 | 165.27 ± 0.75 | -4.64% |
| 1024 | 5565.43 ± 12.14 | 4605.64 ± 10.43 | +20.84% | 157.05 ± 0.17 | 163.82 ± 0.89 | -4.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
