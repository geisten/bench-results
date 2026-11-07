# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1184.32 ± 15.48 | 738.74 ± 9.52 | +60.32% | 79.32 ± 1.13 | 67.85 ± 0.83 | +16.90% |
| 256 | 1206.62 ± 8.15 | 768.12 ± 6.30 | +57.09% | 79.08 ± 1.12 | 67.53 ± 0.54 | +17.10% |
| 512 | 1198.00 ± 7.41 | 779.85 ± 6.47 | +53.62% | 79.89 ± 0.65 | 68.18 ± 0.39 | +17.17% |
| 1024 | 1191.60 ± 6.41 | 846.24 ± 67.68 | +40.81% | 79.56 ± 0.28 | 67.72 ± 0.59 | +17.48% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
