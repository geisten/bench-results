# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8920.79 ± 32.39 | 8540.04 ± 183.81 | +4.46% | 328.37 ± 0.60 | 311.76 ± 0.74 | +5.33% |
| 256 | 11992.04 ± 54.17 | 11559.10 ± 26.10 | +3.75% | 329.38 ± 0.57 | 291.79 ± 0.85 | +12.88% |
| 512 | 15268.09 ± 22.31 | 12104.50 ± 20.50 | +26.14% | 328.70 ± 0.40 | 291.06 ± 2.77 | +12.93% |
| 1024 | 15060.48 ± 26.53 | 11857.80 ± 12.20 | +27.01% | 326.78 ± 0.35 | 282.79 ± 0.96 | +15.55% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
