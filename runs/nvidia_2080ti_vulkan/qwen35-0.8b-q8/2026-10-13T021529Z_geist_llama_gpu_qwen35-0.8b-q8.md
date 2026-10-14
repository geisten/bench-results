# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `db8314e2a3a3`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9025.56 ± 66.33 | 8467.87 ± 132.41 | +6.59% | 325.59 ± 0.23 | 309.25 ± 0.40 | +5.28% |
| 256 | 12265.28 ± 57.65 | 11531.50 ± 33.70 | +6.36% | 326.53 ± 0.27 | 286.52 ± 0.76 | +13.97% |
| 512 | 15687.96 ± 35.54 | 12129.20 ± 30.70 | +29.34% | 326.55 ± 0.64 | 287.30 ± 2.59 | +13.66% |
| 1024 | 15437.40 ± 31.19 | 11857.60 ± 22.35 | +30.19% | 324.46 ± 0.30 | 284.08 ± 1.64 | +14.22% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
