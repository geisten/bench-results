# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a1751c84f0d4`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8885.81 ± 35.94 | 8437.15 ± 206.61 | +5.32% | 329.27 ± 1.62 | 310.99 ± 0.69 | +5.88% |
| 256 | 11962.34 ± 35.50 | 11372.60 ± 190.65 | +5.19% | 330.29 ± 0.89 | 292.21 ± 0.75 | +13.03% |
| 512 | 15287.01 ± 9.59 | 12065.80 ± 26.80 | +26.70% | 330.13 ± 1.29 | 290.83 ± 1.67 | +13.51% |
| 1024 | 15089.45 ± 24.12 | 11825.35 ± 24.65 | +27.60% | 327.60 ± 0.61 | 289.16 ± 1.04 | +13.29% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
