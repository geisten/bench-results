# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `2b5263f87833`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9040.19 ± 51.36 | 7462.68 ± 1058.79 | +21.14% | 327.76 ± 1.58 | 309.69 ± 0.37 | +5.84% |
| 256 | 12277.61 ± 41.98 | 11548.80 ± 59.65 | +6.31% | 329.87 ± 0.44 | 288.91 ± 1.62 | +14.18% |
| 512 | 15675.95 ± 19.94 | 12174.15 ± 36.05 | +28.76% | 329.32 ± 0.55 | 288.51 ± 0.98 | +14.15% |
| 1024 | 15458.12 ± 21.01 | 11894.70 ± 28.10 | +29.96% | 327.93 ± 0.26 | 288.45 ± 1.42 | +13.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
