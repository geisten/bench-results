# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9052.01 ± 23.11 | 7537.54 ± 1149.96 | +20.09% | 327.02 ± 0.39 | 309.55 ± 0.79 | +5.64% |
| 256 | 12325.77 ± 25.86 | 11493.95 ± 129.80 | +7.24% | 327.59 ± 0.43 | 287.96 ± 0.99 | +13.76% |
| 512 | 15684.59 ± 18.52 | 12130.00 ± 34.65 | +29.30% | 327.36 ± 0.15 | 287.11 ± 1.43 | +14.02% |
| 1024 | 15435.52 ± 5.47 | 11841.90 ± 31.15 | +30.35% | 325.88 ± 0.37 | 287.32 ± 2.18 | +13.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
