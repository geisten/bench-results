# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ac9a0f9cf37c`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8910.56 ± 26.43 | 7514.17 ± 1118.70 | +18.58% | 329.29 ± 0.22 | 309.66 ± 0.32 | +6.34% |
| 256 | 11996.53 ± 27.89 | 11571.55 ± 43.70 | +3.67% | 329.72 ± 0.76 | 290.06 ± 0.81 | +13.67% |
| 512 | 15235.15 ± 10.89 | 12154.80 ± 22.95 | +25.34% | 328.93 ± 0.63 | 289.19 ± 1.32 | +13.74% |
| 1024 | 14999.16 ± 12.42 | 11923.30 ± 5.55 | +25.80% | 327.43 ± 0.47 | 288.28 ± 1.72 | +13.58% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
