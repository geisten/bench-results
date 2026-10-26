# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `eedaae6cae7b`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.77 ± 1.62 | 515.93 ± 5.18 | +11.21% | 40.61 ± 0.11 | 28.99 ± 0.04 | +40.07% |
| 256 | 590.12 ± 1.93 | 536.63 ± 5.68 | +9.97% | 40.40 ± 0.08 | 29.24 ± 0.04 | +38.17% |
| 512 | 633.50 ± 3.19 | 547.78 ± 6.05 | +15.65% | 40.08 ± 0.12 | 29.40 ± 0.03 | +36.33% |
| 1024 | 623.99 ± 1.11 | 543.47 ± 5.04 | +14.81% | 39.67 ± 0.06 | 29.23 ± 0.07 | +35.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
