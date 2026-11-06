# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `406a3c0519ec`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8888.89 ± 40.62 | 7586.14 ± 966.51 | +17.17% | 326.45 ± 0.42 | 308.24 ± 0.70 | +5.91% |
| 256 | 11961.79 ± 51.77 | 11428.25 ± 85.95 | +4.67% | 326.94 ± 0.70 | 289.59 ± 0.68 | +12.90% |
| 512 | 15192.43 ± 42.07 | 12092.45 ± 15.05 | +25.64% | 326.09 ± 0.39 | 288.05 ± 1.61 | +13.20% |
| 1024 | 15003.11 ± 14.52 | 11839.20 ± 25.55 | +26.72% | 324.64 ± 0.05 | 287.15 ± 1.69 | +13.06% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
