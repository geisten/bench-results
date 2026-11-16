# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `199d6ecb49dd`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8902.80 ± 52.32 | 7475.01 ± 1125.76 | +19.10% | 328.91 ± 0.90 | 311.04 ± 0.53 | +5.75% |
| 256 | 11986.70 ± 38.73 | 11157.90 ± 452.00 | +7.43% | 329.72 ± 1.30 | 292.12 ± 0.98 | +12.87% |
| 512 | 15246.49 ± 29.45 | 12193.05 ± 17.50 | +25.04% | 328.87 ± 0.80 | 292.42 ± 1.49 | +12.47% |
| 1024 | 15009.49 ± 10.11 | 11860.75 ± 10.20 | +26.55% | 327.29 ± 0.31 | 291.25 ± 1.90 | +12.37% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
