# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `93817e73fce2`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.17 ± 2.03 | 514.70 ± 4.00 | +11.75% | 40.51 ± 0.04 | 29.10 ± 0.04 | +39.20% |
| 256 | 590.26 ± 0.89 | 535.21 ± 4.87 | +10.29% | 40.35 ± 0.06 | 29.14 ± 0.09 | +38.47% |
| 512 | 632.90 ± 2.21 | 547.22 ± 4.62 | +15.66% | 40.01 ± 0.08 | 29.12 ± 0.04 | +37.39% |
| 1024 | 626.24 ± 2.71 | 540.54 ± 4.55 | +15.86% | 39.67 ± 0.12 | 29.28 ± 0.11 | +35.48% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
