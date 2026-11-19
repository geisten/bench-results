# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8904.35 ± 38.57 | 8365.46 ± 322.19 | +6.44% | 328.29 ± 1.36 | 310.64 ± 0.83 | +5.68% |
| 256 | 11982.22 ± 31.43 | 11479.60 ± 89.10 | +4.38% | 328.94 ± 0.55 | 291.33 ± 1.51 | +12.91% |
| 512 | 15261.94 ± 20.70 | 12075.60 ± 25.55 | +26.39% | 328.43 ± 0.40 | 291.11 ± 1.89 | +12.82% |
| 1024 | 15005.86 ± 26.34 | 11840.40 ± 15.20 | +26.73% | 326.83 ± 0.31 | 288.88 ± 3.07 | +13.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
