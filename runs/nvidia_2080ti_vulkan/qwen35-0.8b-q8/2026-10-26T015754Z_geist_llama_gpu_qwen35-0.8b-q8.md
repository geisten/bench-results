# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `eedaae6cae7b`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8926.70 ± 38.45 | 7754.39 ± 862.55 | +15.12% | 326.34 ± 2.10 | 309.68 ± 0.52 | +5.38% |
| 256 | 12021.04 ± 42.90 | 11448.90 ± 40.65 | +5.00% | 328.10 ± 0.72 | 290.14 ± 1.71 | +13.08% |
| 512 | 15270.36 ± 17.07 | 12112.40 ± 30.25 | +26.07% | 326.21 ± 0.90 | 288.71 ± 2.27 | +12.99% |
| 1024 | 15010.70 ± 42.92 | 11865.35 ± 15.60 | +26.51% | 324.14 ± 0.29 | 287.79 ± 1.84 | +12.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
