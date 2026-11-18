# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `372846765fa0`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.34 ± 1.96 | 517.18 ± 6.05 | +11.25% | 40.63 ± 0.04 | 29.08 ± 0.05 | +39.72% |
| 256 | 590.18 ± 1.05 | 535.74 ± 4.88 | +10.16% | 40.49 ± 0.05 | 29.28 ± 0.06 | +38.29% |
| 512 | 632.62 ± 1.74 | 548.31 ± 4.50 | +15.38% | 40.14 ± 0.07 | 29.47 ± 0.14 | +36.22% |
| 1024 | 625.39 ± 1.83 | 543.85 ± 4.80 | +14.99% | 39.82 ± 0.11 | 29.31 ± 0.04 | +35.83% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
