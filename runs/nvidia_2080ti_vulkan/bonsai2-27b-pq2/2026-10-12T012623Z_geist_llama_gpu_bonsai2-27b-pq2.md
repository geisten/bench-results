# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `4d6e2696a51b`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.02 ± 2.42 | 518.16 ± 6.17 | +11.17% | 40.62 ± 0.07 | 29.06 ± 0.19 | +39.81% |
| 256 | 591.36 ± 1.31 | 536.05 ± 4.65 | +10.32% | 40.41 ± 0.10 | 29.26 ± 0.21 | +38.09% |
| 512 | 635.55 ± 1.68 | 548.63 ± 4.49 | +15.84% | 39.98 ± 0.04 | 29.34 ± 0.04 | +36.27% |
| 1024 | 627.63 ± 0.99 | 538.54 ± 4.72 | +16.54% | 39.72 ± 0.12 | 29.32 ± 0.08 | +35.46% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
