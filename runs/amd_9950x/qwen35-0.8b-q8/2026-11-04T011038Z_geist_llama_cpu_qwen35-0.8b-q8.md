# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1707.81 ± 3.08 | 993.90 ± 15.05 | +71.83% | 81.71 ± 0.60 | 70.60 ± 0.29 | +15.74% |
| 256 | 1740.66 ± 7.49 | 1036.76 ± 12.57 | +67.89% | 82.09 ± 0.31 | 69.42 ± 0.49 | +18.25% |
| 512 | 1747.76 ± 12.16 | 1037.89 ± 4.99 | +68.40% | 81.96 ± 0.24 | 69.76 ± 0.89 | +17.49% |
| 1024 | 1726.58 ± 5.23 | 1030.18 ± 3.83 | +67.60% | 81.53 ± 0.27 | 68.98 ± 0.68 | +18.20% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
