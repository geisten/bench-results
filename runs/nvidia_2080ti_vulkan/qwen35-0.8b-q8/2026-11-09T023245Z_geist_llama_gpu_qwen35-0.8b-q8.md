# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8900.94 ± 43.76 | 8191.25 ± 409.79 | +8.66% | 326.64 ± 0.22 | 308.67 ± 0.85 | +5.82% |
| 256 | 12008.91 ± 47.51 | 11471.80 ± 10.15 | +4.68% | 327.13 ± 0.26 | 290.26 ± 0.89 | +12.70% |
| 512 | 15212.06 ± 60.05 | 12114.95 ± 18.30 | +25.56% | 326.11 ± 0.87 | 289.63 ± 1.60 | +12.60% |
| 1024 | 15011.58 ± 6.27 | 11841.65 ± 18.80 | +26.77% | 324.87 ± 0.14 | 288.41 ± 1.88 | +12.64% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
