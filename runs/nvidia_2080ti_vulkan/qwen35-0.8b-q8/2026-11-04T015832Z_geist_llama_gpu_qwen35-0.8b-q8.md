# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8903.15 ± 33.84 | 7460.56 ± 1103.93 | +19.34% | 326.76 ± 1.46 | 308.46 ± 0.81 | +5.93% |
| 256 | 11937.82 ± 35.00 | 11437.90 ± 115.45 | +4.37% | 326.99 ± 0.44 | 289.45 ± 1.23 | +12.97% |
| 512 | 15226.77 ± 43.71 | 12074.45 ± 6.20 | +26.11% | 326.23 ± 0.69 | 288.86 ± 1.58 | +12.94% |
| 1024 | 14999.49 ± 5.60 | 11834.10 ± 15.75 | +26.75% | 324.69 ± 0.10 | 288.08 ± 1.85 | +12.71% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
