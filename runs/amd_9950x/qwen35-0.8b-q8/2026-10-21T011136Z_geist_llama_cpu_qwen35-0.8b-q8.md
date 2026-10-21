# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `24515004c598`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1192.29 ± 18.39 | 734.51 ± 4.34 | +62.32% | 80.12 ± 0.52 | 68.23 ± 0.57 | +17.42% |
| 256 | 1202.54 ± 16.98 | 773.47 ± 3.52 | +55.47% | 79.96 ± 0.57 | 68.35 ± 0.56 | +16.99% |
| 512 | 1198.94 ± 13.95 | 773.24 ± 2.14 | +55.05% | 79.57 ± 0.43 | 68.37 ± 0.36 | +16.38% |
| 1024 | 1209.66 ± 25.99 | 770.32 ± 3.71 | +57.03% | 79.47 ± 0.36 | 67.59 ± 0.47 | +17.59% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
