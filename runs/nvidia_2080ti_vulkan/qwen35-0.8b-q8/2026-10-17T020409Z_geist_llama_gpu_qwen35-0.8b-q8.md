# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b892b0f366c`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9037.64 ± 24.63 | 8312.37 ± 337.14 | +8.73% | 327.24 ± 1.28 | 309.42 ± 0.34 | +5.76% |
| 256 | 12294.10 ± 32.68 | 11170.55 ± 368.05 | +10.06% | 328.21 ± 0.47 | 289.95 ± 0.86 | +13.20% |
| 512 | 15690.61 ± 27.94 | 12150.25 ± 16.15 | +29.14% | 327.53 ± 0.29 | 289.52 ± 1.45 | +13.13% |
| 1024 | 15454.74 ± 12.48 | 11834.45 ± 16.00 | +30.59% | 325.91 ± 0.28 | 287.29 ± 1.14 | +13.44% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
