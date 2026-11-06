# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8890.44 ± 44.05 | 8254.08 ± 374.15 | +7.71% | 326.60 ± 2.74 | 309.12 ± 0.38 | +5.65% |
| 256 | 12024.99 ± 57.73 | 11533.75 ± 50.60 | +4.26% | 328.07 ± 1.19 | 289.35 ± 1.76 | +13.38% |
| 512 | 15258.30 ± 9.32 | 12113.95 ± 34.20 | +25.96% | 327.15 ± 1.01 | 288.42 ± 2.29 | +13.43% |
| 1024 | 15044.11 ± 28.79 | 11849.05 ± 15.15 | +26.96% | 325.19 ± 0.14 | 287.19 ± 2.24 | +13.23% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
