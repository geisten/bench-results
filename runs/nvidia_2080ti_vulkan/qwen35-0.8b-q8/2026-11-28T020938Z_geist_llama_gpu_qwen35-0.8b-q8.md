# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b0ee998e552`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8928.26 ± 31.13 | 7549.42 ± 1111.35 | +18.26% | 329.38 ± 1.78 | 311.52 ± 0.90 | +5.74% |
| 256 | 12004.47 ± 57.75 | 11530.00 ± 117.00 | +4.12% | 331.81 ± 0.58 | 288.95 ± 4.70 | +14.83% |
| 512 | 15253.30 ± 6.59 | 12106.35 ± 31.35 | +25.99% | 328.99 ± 0.80 | 291.26 ± 2.79 | +12.95% |
| 1024 | 15051.96 ± 18.61 | 11879.35 ± 9.30 | +26.71% | 328.26 ± 0.79 | 288.68 ± 2.98 | +13.71% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
