# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `f4ae43569c6a`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.29 ± 2.63 | 516.64 ± 4.78 | +11.55% | 40.75 ± 0.09 | 29.22 ± 0.04 | +39.46% |
| 256 | 592.00 ± 1.33 | 536.16 ± 4.72 | +10.41% | 40.57 ± 0.10 | 29.27 ± 0.08 | +38.63% |
| 512 | 634.42 ± 1.07 | 548.24 ± 5.27 | +15.72% | 40.17 ± 0.07 | 29.56 ± 0.02 | +35.92% |
| 1024 | 627.66 ± 1.89 | 545.63 ± 4.50 | +15.03% | 39.88 ± 0.12 | 29.36 ± 0.08 | +35.85% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
