# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `fda9c7a98c7b`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.13 ± 1.14 | 519.13 ± 4.91 | +10.98% | 40.55 ± 0.04 | 29.03 ± 0.17 | +39.65% |
| 256 | 591.83 ± 1.54 | 535.63 ± 4.34 | +10.49% | 40.43 ± 0.11 | 29.23 ± 0.17 | +38.30% |
| 512 | 635.09 ± 1.53 | 548.95 ± 4.40 | +15.69% | 40.00 ± 0.04 | 29.35 ± 0.03 | +36.28% |
| 1024 | 627.32 ± 1.16 | 538.91 ± 4.17 | +16.40% | 39.73 ± 0.09 | 29.33 ± 0.10 | +35.44% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
