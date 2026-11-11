# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8918.64 ± 40.89 | 8470.09 ± 174.27 | +5.30% | 326.58 ± 1.27 | 309.31 ± 0.40 | +5.58% |
| 256 | 11992.32 ± 69.78 | 11476.25 ± 111.00 | +4.50% | 327.10 ± 0.27 | 289.26 ± 1.79 | +13.08% |
| 512 | 15222.93 ± 36.97 | 12093.05 ± 27.30 | +25.88% | 326.59 ± 0.52 | 289.01 ± 1.66 | +13.00% |
| 1024 | 14995.53 ± 10.88 | 11822.90 ± 20.05 | +26.83% | 324.87 ± 0.34 | 287.44 ± 1.60 | +13.02% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
