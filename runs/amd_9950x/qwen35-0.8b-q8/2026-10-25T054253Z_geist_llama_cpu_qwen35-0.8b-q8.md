# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1197.71 ± 18.50 | 735.07 ± 4.15 | +62.94% | 79.72 ± 0.26 | 68.63 ± 0.83 | +16.15% |
| 256 | 1190.22 ± 8.42 | 770.09 ± 2.49 | +54.56% | 79.78 ± 0.29 | 69.46 ± 0.32 | +14.86% |
| 512 | 1183.24 ± 9.58 | 775.90 ± 1.14 | +52.50% | 79.92 ± 0.60 | 68.93 ± 0.60 | +15.95% |
| 1024 | 1189.09 ± 14.55 | 770.49 ± 3.99 | +54.33% | 79.47 ± 0.89 | 68.38 ± 0.74 | +16.21% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
