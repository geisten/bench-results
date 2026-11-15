# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8912.10 ± 30.19 | 7448.76 ± 1105.94 | +19.65% | 326.53 ± 0.39 | 308.57 ± 0.83 | +5.82% |
| 256 | 12015.40 ± 50.98 | 11564.35 ± 23.35 | +3.90% | 327.16 ± 0.45 | 288.13 ± 1.83 | +13.55% |
| 512 | 15239.68 ± 8.85 | 12122.25 ± 18.55 | +25.72% | 326.49 ± 0.38 | 287.91 ± 1.78 | +13.40% |
| 1024 | 14998.72 ± 12.30 | 11837.50 ± 18.40 | +26.71% | 325.08 ± 0.22 | 286.50 ± 2.39 | +13.47% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
