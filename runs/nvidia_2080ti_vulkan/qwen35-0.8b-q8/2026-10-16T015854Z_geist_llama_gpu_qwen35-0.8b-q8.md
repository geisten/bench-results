# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `fda9c7a98c7b`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9042.11 ± 46.22 | 7478.58 ± 1131.22 | +20.91% | 325.43 ± 1.50 | 309.26 ± 0.29 | +5.23% |
| 256 | 12238.56 ± 60.82 | 11510.45 ± 51.80 | +6.33% | 326.60 ± 0.18 | 287.47 ± 1.98 | +13.61% |
| 512 | 15679.07 ± 18.48 | 12087.20 ± 37.85 | +29.72% | 325.99 ± 0.84 | 285.43 ± 1.65 | +14.21% |
| 1024 | 15410.78 ± 14.27 | 11841.60 ± 25.25 | +30.14% | 324.90 ± 0.74 | 283.68 ± 1.40 | +14.53% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
