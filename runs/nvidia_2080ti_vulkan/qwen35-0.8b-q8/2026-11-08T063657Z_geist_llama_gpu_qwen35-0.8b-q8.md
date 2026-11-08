# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8908.39 ± 36.72 | 7449.15 ± 1106.54 | +19.59% | 326.72 ± 0.33 | 309.20 ± 0.72 | +5.67% |
| 256 | 11979.98 ± 34.18 | 11468.65 ± 57.85 | +4.46% | 327.26 ± 0.17 | 289.52 ± 0.25 | +13.04% |
| 512 | 15271.05 ± 18.47 | 12094.05 ± 16.55 | +26.27% | 326.53 ± 0.89 | 288.16 ± 2.00 | +13.32% |
| 1024 | 15013.78 ± 8.15 | 11839.75 ± 17.45 | +26.81% | 324.94 ± 0.16 | 285.81 ± 1.92 | +13.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
