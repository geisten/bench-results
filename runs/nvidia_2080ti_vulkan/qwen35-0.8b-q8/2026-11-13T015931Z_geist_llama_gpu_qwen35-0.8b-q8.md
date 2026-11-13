# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8934.18 ± 26.58 | 7825.14 ± 776.57 | +14.17% | 326.42 ± 0.83 | 309.19 ± 0.45 | +5.57% |
| 256 | 11997.12 ± 75.46 | 11486.60 ± 10.80 | +4.44% | 327.12 ± 0.52 | 286.47 ± 1.05 | +14.19% |
| 512 | 15278.57 ± 6.39 | 12116.90 ± 17.55 | +26.09% | 326.57 ± 0.56 | 286.16 ± 1.76 | +14.12% |
| 1024 | 15043.90 ± 34.19 | 11850.65 ± 22.90 | +26.95% | 324.97 ± 0.32 | 286.95 ± 2.49 | +13.25% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
