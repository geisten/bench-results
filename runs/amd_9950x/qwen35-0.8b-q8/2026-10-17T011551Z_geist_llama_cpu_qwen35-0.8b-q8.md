# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b892b0f366c`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1202.19 ± 26.33 | 742.75 ± 4.16 | +61.86% | 80.56 ± 0.36 | 69.21 ± 0.30 | +16.40% |
| 256 | 1225.57 ± 30.94 | 768.51 ± 4.17 | +59.47% | 80.38 ± 0.35 | 69.13 ± 0.77 | +16.27% |
| 512 | 1216.68 ± 29.07 | 776.85 ± 2.34 | +56.62% | 80.22 ± 0.34 | 69.83 ± 0.44 | +14.88% |
| 1024 | 1198.38 ± 18.35 | 772.25 ± 4.31 | +55.18% | 79.91 ± 0.36 | 67.75 ± 0.41 | +17.94% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
