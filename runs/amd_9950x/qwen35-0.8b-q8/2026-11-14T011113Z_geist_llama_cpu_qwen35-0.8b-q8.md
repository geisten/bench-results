# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1693.45 ± 11.32 | 997.42 ± 7.43 | +69.78% | 82.19 ± 0.18 | 70.31 ± 0.40 | +16.89% |
| 256 | 1728.70 ± 8.60 | 1036.20 ± 5.46 | +66.83% | 82.01 ± 0.24 | 70.93 ± 0.66 | +15.63% |
| 512 | 1742.49 ± 20.38 | 1046.94 ± 10.88 | +66.44% | 81.74 ± 0.29 | 69.08 ± 0.55 | +18.33% |
| 1024 | 1736.40 ± 9.85 | 1023.89 ± 17.97 | +69.59% | 81.40 ± 0.29 | 69.37 ± 0.62 | +17.33% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
