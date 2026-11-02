# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f83e03b37679`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8911.17 ± 25.81 | 7495.91 ± 1144.80 | +18.88% | 326.40 ± 0.63 | 309.29 ± 0.49 | +5.53% |
| 256 | 12035.45 ± 52.09 | 11539.30 ± 61.90 | +4.30% | 327.58 ± 0.67 | 289.00 ± 1.51 | +13.35% |
| 512 | 15229.71 ± 18.33 | 12108.65 ± 36.70 | +25.78% | 327.18 ± 1.48 | 289.29 ± 1.33 | +13.10% |
| 1024 | 14992.90 ± 11.08 | 11891.85 ± 35.10 | +26.08% | 326.57 ± 1.35 | 288.20 ± 1.58 | +13.31% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
