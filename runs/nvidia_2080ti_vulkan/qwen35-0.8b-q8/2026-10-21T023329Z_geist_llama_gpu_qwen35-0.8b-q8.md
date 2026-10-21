# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `5afe43c5b436`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9029.03 ± 62.85 | 7646.39 ± 982.64 | +18.08% | 328.14 ± 1.50 | 309.39 ± 0.38 | +6.06% |
| 256 | 12244.12 ± 39.82 | 11587.00 ± 21.25 | +5.67% | 330.12 ± 0.55 | 289.32 ± 0.40 | +14.10% |
| 512 | 15687.96 ± 34.37 | 12149.50 ± 42.60 | +29.12% | 330.00 ± 0.38 | 289.21 ± 1.27 | +14.11% |
| 1024 | 15426.57 ± 12.20 | 11895.45 ± 19.35 | +29.68% | 328.40 ± 0.15 | 288.59 ± 1.56 | +13.79% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
