# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `14ac9f78e1df`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9029.66 ± 42.56 | 7509.95 ± 1103.19 | +20.24% | 327.95 ± 2.04 | 309.27 ± 0.65 | +6.04% |
| 256 | 12201.23 ± 73.59 | 11543.00 ± 49.70 | +5.70% | 330.38 ± 0.55 | 286.65 ± 2.66 | +15.26% |
| 512 | 15681.95 ± 33.87 | 12147.70 ± 17.95 | +29.09% | 329.44 ± 0.62 | 287.28 ± 2.53 | +14.68% |
| 1024 | 15427.38 ± 14.18 | 11880.55 ± 12.80 | +29.85% | 327.48 ± 0.74 | 286.06 ± 2.25 | +14.48% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
