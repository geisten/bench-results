# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8884.92 ± 59.88 | 7902.60 ± 711.25 | +12.43% | 326.88 ± 2.50 | 308.71 ± 1.00 | +5.89% |
| 256 | 11990.35 ± 19.92 | 11477.05 ± 117.95 | +4.47% | 328.89 ± 0.49 | 290.29 ± 0.71 | +13.30% |
| 512 | 15275.15 ± 17.34 | 12162.85 ± 15.50 | +25.59% | 329.11 ± 0.54 | 289.40 ± 1.44 | +13.72% |
| 1024 | 15003.56 ± 23.55 | 11925.10 ± 15.20 | +25.81% | 326.85 ± 0.73 | 288.62 ± 1.80 | +13.25% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
