# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `cdc4ba43c58a`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9037.03 ± 36.72 | 7496.15 ± 1117.02 | +20.56% | 327.49 ± 1.07 | 309.01 ± 0.36 | +5.98% |
| 256 | 12331.12 ± 74.39 | 11578.45 ± 25.95 | +6.50% | 327.67 ± 0.61 | 287.33 ± 2.17 | +14.04% |
| 512 | 15679.31 ± 19.45 | 12111.35 ± 30.95 | +29.46% | 326.90 ± 0.98 | 285.30 ± 1.13 | +14.58% |
| 1024 | 15406.49 ± 6.03 | 11821.50 ± 26.60 | +30.33% | 325.45 ± 0.22 | 284.33 ± 1.24 | +14.46% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
