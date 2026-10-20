# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `44479afd263d`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9023.62 ± 65.36 | 7549.52 ± 1135.01 | +19.53% | 328.66 ± 0.61 | 309.17 ± 0.80 | +6.31% |
| 256 | 12251.73 ± 40.62 | 11560.95 ± 56.50 | +5.98% | 328.75 ± 0.89 | 287.84 ± 1.57 | +14.21% |
| 512 | 15714.20 ± 26.81 | 12194.45 ± 28.65 | +28.86% | 328.95 ± 0.98 | 286.83 ± 1.83 | +14.69% |
| 1024 | 15476.46 ± 10.77 | 11899.50 ± 17.20 | +30.06% | 328.19 ± 0.31 | 286.00 ± 2.15 | +14.75% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
