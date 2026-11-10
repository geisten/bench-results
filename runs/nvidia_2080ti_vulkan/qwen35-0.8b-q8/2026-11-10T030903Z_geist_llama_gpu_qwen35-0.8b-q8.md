# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8877.18 ± 45.17 | 7435.20 ± 1114.20 | +19.39% | 326.38 ± 2.34 | 309.58 ± 0.22 | +5.43% |
| 256 | 12016.80 ± 34.73 | 11415.95 ± 119.00 | +5.26% | 327.36 ± 1.21 | 289.51 ± 1.60 | +13.07% |
| 512 | 15258.30 ± 17.27 | 12090.40 ± 11.45 | +26.20% | 326.80 ± 0.38 | 286.46 ± 1.53 | +14.08% |
| 1024 | 15045.33 ± 23.02 | 11850.40 ± 33.15 | +26.96% | 325.22 ± 0.24 | 283.50 ± 1.07 | +14.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
