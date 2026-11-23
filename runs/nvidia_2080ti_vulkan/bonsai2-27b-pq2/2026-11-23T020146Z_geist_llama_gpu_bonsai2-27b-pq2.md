# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `a1751c84f0d4`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.70 ± 1.44 | 516.32 ± 5.13 | +11.50% | 40.66 ± 0.04 | 29.19 ± 0.07 | +39.26% |
| 256 | 591.02 ± 0.81 | 536.16 ± 4.63 | +10.23% | 40.50 ± 0.05 | 29.19 ± 0.09 | +38.76% |
| 512 | 632.91 ± 0.81 | 549.98 ± 4.86 | +15.08% | 40.17 ± 0.05 | 29.52 ± 0.07 | +36.08% |
| 1024 | 626.83 ± 2.10 | 545.91 ± 4.65 | +14.82% | 39.88 ± 0.13 | 29.38 ± 0.09 | +35.74% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
