# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `a4d332c604a2`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.28 ± 2.25 | 514.93 ± 4.03 | +11.52% | 40.57 ± 0.06 | 28.90 ± 0.10 | +40.37% |
| 256 | 588.67 ± 1.26 | 535.50 ± 4.59 | +9.93% | 40.30 ± 0.10 | 28.92 ± 0.09 | +39.35% |
| 512 | 633.06 ± 1.41 | 548.37 ± 5.20 | +15.44% | 40.03 ± 0.04 | 29.66 ± 0.06 | +34.99% |
| 1024 | 625.56 ± 1.75 | 544.53 ± 5.74 | +14.88% | 39.66 ± 0.06 | 29.37 ± 0.04 | +35.05% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
