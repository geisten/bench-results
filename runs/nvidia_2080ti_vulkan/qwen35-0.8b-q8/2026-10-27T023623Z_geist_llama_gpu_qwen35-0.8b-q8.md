# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `df665fe9c736`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8883.95 ± 34.67 | 7523.31 ± 1122.15 | +18.09% | 326.76 ± 1.60 | 309.94 ± 0.30 | +5.43% |
| 256 | 12036.87 ± 44.87 | 11523.60 ± 34.50 | +4.45% | 328.34 ± 0.44 | 287.05 ± 1.04 | +14.38% |
| 512 | 15270.14 ± 22.35 | 12114.45 ± 18.90 | +26.05% | 328.23 ± 0.41 | 286.99 ± 1.72 | +14.37% |
| 1024 | 15040.80 ± 22.31 | 11858.35 ± 16.40 | +26.84% | 326.55 ± 0.08 | 285.19 ± 1.52 | +14.50% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
