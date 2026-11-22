# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8895.38 ± 49.21 | 7497.08 ± 1139.15 | +18.65% | 329.95 ± 1.80 | 311.76 ± 0.61 | +5.83% |
| 256 | 11992.04 ± 40.02 | 11539.45 ± 33.60 | +3.92% | 330.85 ± 1.00 | 284.66 ± 2.35 | +16.23% |
| 512 | 15272.87 ± 12.30 | 12139.45 ± 36.00 | +25.81% | 329.69 ± 0.95 | 289.62 ± 2.71 | +13.83% |
| 1024 | 15014.11 ± 22.88 | 11872.25 ± 19.45 | +26.46% | 329.24 ± 0.94 | 288.56 ± 2.45 | +14.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
