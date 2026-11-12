# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8900.02 ± 46.33 | 7461.08 ± 1100.86 | +19.29% | 326.54 ± 0.47 | 308.49 ± 0.96 | +5.85% |
| 256 | 12022.73 ± 35.19 | 11471.75 ± 38.80 | +4.80% | 327.23 ± 0.57 | 289.58 ± 0.69 | +13.00% |
| 512 | 15238.10 ± 35.00 | 12124.55 ± 28.80 | +25.68% | 326.34 ± 0.42 | 288.52 ± 1.51 | +13.11% |
| 1024 | 14991.58 ± 6.70 | 11844.90 ± 16.25 | +26.57% | 324.63 ± 0.14 | 287.62 ± 1.88 | +12.87% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
