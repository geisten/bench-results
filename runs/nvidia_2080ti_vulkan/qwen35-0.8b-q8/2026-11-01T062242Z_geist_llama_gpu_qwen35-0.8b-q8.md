# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8907.15 ± 61.46 | 7515.53 ± 1106.91 | +18.52% | 327.08 ± 2.05 | 309.23 ± 1.09 | +5.77% |
| 256 | 12038.85 ± 79.02 | 11538.80 ± 26.60 | +4.33% | 328.41 ± 0.78 | 285.99 ± 0.70 | +14.83% |
| 512 | 15256.94 ± 15.93 | 12182.50 ± 30.70 | +25.24% | 327.46 ± 1.32 | 286.21 ± 1.26 | +14.41% |
| 1024 | 15002.56 ± 12.75 | 11889.70 ± 15.60 | +26.18% | 326.89 ± 0.59 | 284.71 ± 1.49 | +14.82% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
