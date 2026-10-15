# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ebcdfb017ba6`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9038.59 ± 40.59 | 7486.90 ± 1118.03 | +20.73% | 325.56 ± 0.35 | 309.15 ± 0.64 | +5.31% |
| 256 | 12249.10 ± 43.66 | 11453.20 ± 110.80 | +6.95% | 326.56 ± 0.27 | 290.02 ± 0.67 | +12.60% |
| 512 | 15682.91 ± 25.70 | 12126.40 ± 41.75 | +29.33% | 326.05 ± 0.42 | 289.30 ± 1.22 | +12.70% |
| 1024 | 15461.74 ± 15.89 | 11838.00 ± 24.40 | +30.61% | 324.25 ± 0.14 | 286.82 ± 1.79 | +13.05% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
