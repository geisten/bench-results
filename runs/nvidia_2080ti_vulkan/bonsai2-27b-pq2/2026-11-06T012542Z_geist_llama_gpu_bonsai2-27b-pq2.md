# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `49ffbf5118ee`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.93 ± 1.73 | 515.10 ± 5.44 | +11.42% | 40.53 ± 0.04 | 28.91 ± 0.05 | +40.22% |
| 256 | 590.23 ± 1.67 | 535.00 ± 5.34 | +10.32% | 40.34 ± 0.05 | 28.95 ± 0.07 | +39.35% |
| 512 | 631.41 ± 1.51 | 542.70 ± 4.04 | +16.35% | 39.96 ± 0.03 | 29.61 ± 0.02 | +34.97% |
| 1024 | 623.91 ± 1.03 | 543.04 ± 5.42 | +14.89% | 39.63 ± 0.09 | 29.35 ± 0.03 | +35.03% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
