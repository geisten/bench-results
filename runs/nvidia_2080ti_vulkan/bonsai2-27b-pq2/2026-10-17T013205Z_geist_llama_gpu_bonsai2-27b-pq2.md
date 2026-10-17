# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `0b892b0f366c`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.87 ± 2.15 | 514.33 ± 4.84 | +12.16% | 40.64 ± 0.07 | 29.26 ± 0.07 | +38.89% |
| 256 | 592.63 ± 2.14 | 535.33 ± 4.83 | +10.70% | 40.49 ± 0.11 | 29.61 ± 0.05 | +36.74% |
| 512 | 635.20 ± 1.03 | 548.29 ± 3.95 | +15.85% | 40.10 ± 0.04 | 29.56 ± 0.04 | +35.64% |
| 1024 | 627.30 ± 1.23 | 540.72 ± 4.45 | +16.01% | 39.83 ± 0.12 | 29.59 ± 0.04 | +34.62% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
