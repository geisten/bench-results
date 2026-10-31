# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8928.57 ± 26.55 | 7500.20 ± 1097.62 | +19.04% | 326.63 ± 1.23 | 309.51 ± 0.76 | +5.53% |
| 256 | 11996.53 ± 22.73 | 11459.25 ± 59.15 | +4.69% | 327.72 ± 1.00 | 287.38 ± 1.88 | +14.04% |
| 512 | 15281.76 ± 9.35 | 12142.25 ± 15.75 | +25.86% | 327.37 ± 0.47 | 288.19 ± 1.50 | +13.59% |
| 1024 | 15033.32 ± 25.59 | 11840.25 ± 27.35 | +26.97% | 325.31 ± 0.38 | 286.19 ± 2.55 | +13.67% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
