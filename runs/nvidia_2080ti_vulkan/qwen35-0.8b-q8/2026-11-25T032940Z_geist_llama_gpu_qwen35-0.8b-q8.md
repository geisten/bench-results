# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8860.89 ± 58.66 | 7537.01 ± 1131.15 | +17.57% | 329.15 ± 1.95 | 310.69 ± 0.87 | +5.94% |
| 256 | 11921.40 ± 51.62 | 11577.50 ± 77.20 | +2.97% | 329.49 ± 1.00 | 283.98 ± 1.02 | +16.03% |
| 512 | 15285.87 ± 25.10 | 12117.15 ± 11.20 | +26.15% | 329.01 ± 0.84 | 289.53 ± 3.62 | +13.64% |
| 1024 | 15070.69 ± 28.62 | 11843.10 ± 30.50 | +27.25% | 327.37 ± 0.28 | 288.59 ± 1.92 | +13.44% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
