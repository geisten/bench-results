# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `df665fe9c736`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.74 ± 3.10 | 517.30 ± 4.78 | +11.11% | 40.50 ± 0.06 | 29.27 ± 0.10 | +38.38% |
| 256 | 589.47 ± 1.89 | 536.88 ± 4.43 | +9.80% | 40.34 ± 0.10 | 29.03 ± 0.13 | +38.97% |
| 512 | 631.62 ± 2.48 | 547.40 ± 4.31 | +15.38% | 39.98 ± 0.09 | 29.46 ± 0.13 | +35.73% |
| 1024 | 623.91 ± 1.47 | 544.43 ± 4.92 | +14.60% | 39.66 ± 0.13 | 29.43 ± 0.05 | +34.76% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
