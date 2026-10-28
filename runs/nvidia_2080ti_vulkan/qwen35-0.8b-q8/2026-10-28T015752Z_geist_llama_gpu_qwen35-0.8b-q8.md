# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `13921becb240`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8896.31 ± 38.49 | 7773.55 ± 838.19 | +14.44% | 325.18 ± 1.94 | 309.16 ± 0.54 | +5.18% |
| 256 | 12017.37 ± 28.14 | 11384.60 ± 154.75 | +5.56% | 325.86 ± 0.85 | 289.88 ± 1.00 | +12.41% |
| 512 | 15235.84 ± 23.34 | 12075.95 ± 17.80 | +26.17% | 325.29 ± 1.04 | 288.81 ± 2.04 | +12.63% |
| 1024 | 15008.17 ± 10.01 | 11795.35 ± 12.35 | +27.24% | 323.60 ± 0.25 | 286.36 ± 2.76 | +13.00% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
