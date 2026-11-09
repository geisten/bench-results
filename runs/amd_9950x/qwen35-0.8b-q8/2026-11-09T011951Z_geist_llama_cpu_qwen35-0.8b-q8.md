# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1710.84 ± 11.97 | 983.18 ± 2.51 | +74.01% | 82.20 ± 0.46 | 69.85 ± 0.29 | +17.67% |
| 256 | 1728.82 ± 18.12 | 1029.10 ± 4.65 | +67.99% | 81.73 ± 0.16 | 69.48 ± 0.65 | +17.63% |
| 512 | 1740.00 ± 11.82 | 1013.32 ± 33.80 | +71.71% | 81.67 ± 0.23 | 69.87 ± 0.35 | +16.88% |
| 1024 | 1740.04 ± 8.98 | 997.88 ± 10.60 | +74.37% | 81.55 ± 0.39 | 69.51 ± 0.42 | +17.32% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
