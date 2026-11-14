# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8863.76 ± 94.18 | 7443.24 ± 1095.71 | +19.08% | 326.53 ± 0.75 | 309.18 ± 0.80 | +5.61% |
| 256 | 12051.88 ± 39.28 | 11472.00 ± 19.60 | +5.05% | 327.21 ± 0.83 | 290.02 ± 1.02 | +12.82% |
| 512 | 15267.18 ± 20.94 | 12101.05 ± 16.60 | +26.16% | 326.94 ± 0.27 | 287.07 ± 2.23 | +13.89% |
| 1024 | 15052.85 ± 40.14 | 11856.25 ± 15.90 | +26.96% | 324.79 ± 0.59 | 286.68 ± 2.47 | +13.29% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
