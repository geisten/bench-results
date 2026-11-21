# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8890.44 ± 40.16 | 7795.40 ± 868.64 | +14.05% | 329.16 ± 2.45 | 311.48 ± 1.14 | +5.68% |
| 256 | 11960.40 ± 58.38 | 11523.70 ± 45.25 | +3.79% | 330.09 ± 0.77 | 284.21 ± 1.96 | +16.14% |
| 512 | 15284.49 ± 10.73 | 12103.95 ± 26.15 | +26.28% | 329.40 ± 1.11 | 290.42 ± 2.15 | +13.42% |
| 1024 | 15009.05 ± 10.00 | 11878.95 ± 17.80 | +26.35% | 327.07 ± 0.35 | 287.03 ± 3.30 | +13.95% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
