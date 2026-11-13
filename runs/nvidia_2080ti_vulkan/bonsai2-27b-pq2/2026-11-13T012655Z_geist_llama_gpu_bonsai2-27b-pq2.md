# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `0b27a7bb678a`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.18 ± 1.70 | 514.95 ± 5.68 | +11.50% | 40.53 ± 0.05 | 28.89 ± 0.03 | +40.26% |
| 256 | 590.53 ± 1.43 | 534.90 ± 5.01 | +10.40% | 40.36 ± 0.05 | 28.95 ± 0.07 | +39.42% |
| 512 | 632.32 ± 2.33 | 543.42 ± 4.72 | +16.36% | 40.00 ± 0.05 | 29.66 ± 0.08 | +34.86% |
| 1024 | 624.85 ± 1.78 | 543.06 ± 5.03 | +15.06% | 39.71 ± 0.15 | 29.32 ± 0.09 | +35.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
