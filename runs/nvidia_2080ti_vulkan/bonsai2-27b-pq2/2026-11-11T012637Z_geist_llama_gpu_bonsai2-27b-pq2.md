# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `64c3d9c4227e`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.50 ± 1.20 | 515.29 ± 4.61 | +11.49% | 40.58 ± 0.09 | 28.98 ± 0.07 | +40.03% |
| 256 | 588.08 ± 0.80 | 535.27 ± 4.85 | +9.87% | 40.29 ± 0.09 | 28.90 ± 0.08 | +39.38% |
| 512 | 633.31 ± 1.21 | 543.83 ± 4.11 | +16.45% | 40.01 ± 0.03 | 29.71 ± 0.08 | +34.65% |
| 1024 | 624.99 ± 1.44 | 544.26 ± 5.90 | +14.83% | 39.66 ± 0.08 | 29.39 ± 0.04 | +34.94% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
