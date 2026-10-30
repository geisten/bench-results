# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8891.98 ± 34.41 | 7449.19 ± 1096.94 | +19.37% | 325.35 ± 2.06 | 308.44 ± 0.83 | +5.48% |
| 256 | 11955.65 ± 72.01 | 11466.35 ± 56.50 | +4.27% | 326.35 ± 1.37 | 288.96 ± 1.91 | +12.94% |
| 512 | 15187.25 ± 30.84 | 12091.80 ± 16.70 | +25.60% | 325.31 ± 1.23 | 287.21 ± 2.36 | +13.27% |
| 1024 | 15008.39 ± 12.31 | 11794.45 ± 10.60 | +27.25% | 323.67 ± 0.23 | 288.86 ± 1.62 | +12.05% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
