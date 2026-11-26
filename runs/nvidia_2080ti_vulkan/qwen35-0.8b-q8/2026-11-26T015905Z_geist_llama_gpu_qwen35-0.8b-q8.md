# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8908.69 ± 37.98 | 7532.88 ± 1134.89 | +18.26% | 328.66 ± 1.77 | 310.91 ± 0.62 | +5.71% |
| 256 | 11979.44 ± 35.67 | 11546.20 ± 103.20 | +3.75% | 329.55 ± 0.38 | 288.28 ± 4.76 | +14.32% |
| 512 | 15277.20 ± 25.53 | 12117.85 ± 11.50 | +26.07% | 328.79 ± 1.03 | 287.18 ± 3.61 | +14.49% |
| 1024 | 15058.16 ± 9.41 | 11846.80 ± 11.30 | +27.11% | 327.09 ± 0.26 | 286.48 ± 4.45 | +14.18% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
