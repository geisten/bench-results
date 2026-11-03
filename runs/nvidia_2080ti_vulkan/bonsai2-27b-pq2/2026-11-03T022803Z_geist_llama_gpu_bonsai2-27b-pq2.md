# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `c8df6888df6a`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.25 ± 3.02 | 516.46 ± 5.70 | +11.19% | 40.51 ± 0.09 | 29.30 ± 0.09 | +38.26% |
| 256 | 588.58 ± 1.24 | 536.07 ± 5.63 | +9.80% | 40.29 ± 0.07 | 29.59 ± 0.04 | +36.15% |
| 512 | 632.41 ± 1.90 | 548.60 ± 4.56 | +15.28% | 39.98 ± 0.09 | 29.54 ± 0.06 | +35.34% |
| 1024 | 623.41 ± 1.04 | 539.95 ± 4.07 | +15.46% | 39.59 ± 0.04 | 29.67 ± 0.05 | +33.41% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
