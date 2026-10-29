# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `c212773b0268`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8883.34 ± 72.10 | 7458.22 ± 1122.19 | +19.11% | 325.53 ± 0.91 | 309.27 ± 0.40 | +5.26% |
| 256 | 12098.87 ± 60.02 | 11424.40 ± 147.05 | +5.90% | 327.09 ± 1.09 | 286.31 ± 1.01 | +14.24% |
| 512 | 15281.53 ± 19.64 | 12088.05 ± 12.20 | +26.42% | 326.11 ± 0.35 | 285.62 ± 0.96 | +14.17% |
| 1024 | 15022.81 ± 64.30 | 11923.70 ± 21.20 | +25.99% | 323.56 ± 0.48 | 285.98 ± 1.62 | +13.14% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
