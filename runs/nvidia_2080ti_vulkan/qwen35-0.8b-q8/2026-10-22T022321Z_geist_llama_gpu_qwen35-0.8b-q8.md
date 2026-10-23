# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f19377734f16`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9043.70 ± 42.37 | 8263.47 ± 414.19 | +9.44% | 326.33 ± 2.50 | 308.25 ± 0.99 | +5.87% |
| 256 | 12240.62 ± 51.42 | 11141.80 ± 456.00 | +9.86% | 327.32 ± 0.27 | 288.23 ± 1.07 | +13.56% |
| 512 | 15692.52 ± 12.27 | 12140.60 ± 20.75 | +29.26% | 326.51 ± 0.85 | 287.33 ± 1.14 | +13.64% |
| 1024 | 15431.10 ± 14.17 | 11804.45 ± 35.85 | +30.72% | 325.33 ± 0.58 | 288.04 ± 1.48 | +12.95% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
