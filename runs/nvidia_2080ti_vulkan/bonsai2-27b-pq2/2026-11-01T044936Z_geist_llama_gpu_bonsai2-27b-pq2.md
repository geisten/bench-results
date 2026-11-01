# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `6642260d55a1`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.51 ± 2.79 | 515.81 ± 5.92 | +11.38% | 40.53 ± 0.05 | 29.07 ± 0.05 | +39.40% |
| 256 | 590.10 ± 1.33 | 535.94 ± 5.39 | +10.11% | 40.34 ± 0.03 | 29.17 ± 0.06 | +38.31% |
| 512 | 632.96 ± 2.71 | 545.51 ± 3.94 | +16.03% | 39.99 ± 0.10 | 29.04 ± 0.08 | +37.69% |
| 1024 | 624.19 ± 1.18 | 542.19 ± 6.61 | +15.12% | 39.63 ± 0.08 | 29.22 ± 0.02 | +35.60% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
