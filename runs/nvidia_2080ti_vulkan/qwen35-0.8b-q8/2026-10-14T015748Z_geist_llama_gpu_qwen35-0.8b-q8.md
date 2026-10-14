# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `527bf29dd426`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9030.96 ± 39.34 | 8378.63 ± 278.08 | +7.79% | 325.46 ± 0.37 | 309.22 ± 0.41 | +5.25% |
| 256 | 12246.17 ± 48.70 | 11278.50 ± 308.95 | +8.58% | 326.56 ± 0.40 | 288.32 ± 2.25 | +13.26% |
| 512 | 15679.07 ± 27.37 | 12066.35 ± 28.65 | +29.94% | 325.78 ± 0.69 | 287.50 ± 1.93 | +13.31% |
| 1024 | 15421.92 ± 21.57 | 11827.30 ± 29.35 | +30.39% | 324.50 ± 0.26 | 287.43 ± 1.94 | +12.90% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
