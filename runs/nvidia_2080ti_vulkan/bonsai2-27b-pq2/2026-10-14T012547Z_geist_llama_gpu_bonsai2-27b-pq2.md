# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `527bf29dd426`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.85 ± 1.92 | 519.57 ± 5.40 | +11.02% | 40.57 ± 0.08 | 29.04 ± 0.06 | +39.71% |
| 256 | 592.10 ± 1.82 | 536.23 ± 4.63 | +10.42% | 40.45 ± 0.12 | 29.18 ± 0.12 | +38.60% |
| 512 | 635.36 ± 1.17 | 548.15 ± 4.74 | +15.91% | 40.03 ± 0.09 | 29.35 ± 0.13 | +36.36% |
| 1024 | 627.62 ± 1.24 | 541.40 ± 3.27 | +15.93% | 39.73 ± 0.12 | 29.34 ± 0.11 | +35.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
