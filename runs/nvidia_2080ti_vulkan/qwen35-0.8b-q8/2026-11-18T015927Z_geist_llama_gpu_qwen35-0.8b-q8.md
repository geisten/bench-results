# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8886.12 ± 28.46 | 7500.43 ± 1145.17 | +18.47% | 328.64 ± 1.11 | 310.90 ± 0.38 | +5.71% |
| 256 | 11966.26 ± 24.35 | 11401.55 ± 185.10 | +4.95% | 329.52 ± 0.66 | 285.05 ± 0.79 | +15.60% |
| 512 | 15245.58 ± 20.65 | 12059.10 ± 16.70 | +26.42% | 328.87 ± 1.17 | 285.89 ± 2.05 | +15.03% |
| 1024 | 14993.23 ± 15.90 | 11846.10 ± 15.05 | +26.57% | 327.78 ± 1.26 | 285.42 ± 1.78 | +14.84% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
