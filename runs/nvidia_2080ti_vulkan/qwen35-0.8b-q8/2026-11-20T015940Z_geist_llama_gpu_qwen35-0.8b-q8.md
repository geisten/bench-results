# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8900.94 ± 69.24 | 8047.69 ± 565.48 | +10.60% | 328.28 ± 2.60 | 310.25 ± 0.63 | +5.81% |
| 256 | 12020.19 ± 29.10 | 11515.10 ± 34.30 | +4.39% | 329.12 ± 1.25 | 290.69 ± 1.75 | +13.22% |
| 512 | 15211.62 ± 28.91 | 12074.65 ± 14.35 | +25.98% | 328.08 ± 0.71 | 290.45 ± 1.83 | +12.96% |
| 1024 | 15005.20 ± 12.87 | 11820.20 ± 9.15 | +26.95% | 326.56 ± 0.37 | 289.30 ± 1.87 | +12.88% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
