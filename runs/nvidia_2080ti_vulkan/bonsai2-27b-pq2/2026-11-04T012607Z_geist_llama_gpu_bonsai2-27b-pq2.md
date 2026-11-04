# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `13cb783eddd2`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.51 ± 1.50 | 514.87 ± 5.12 | +11.59% | 40.51 ± 0.05 | 29.17 ± 0.05 | +38.85% |
| 256 | 588.00 ± 1.04 | 535.34 ± 4.54 | +9.84% | 40.26 ± 0.09 | 29.44 ± 0.06 | +36.76% |
| 512 | 632.95 ± 1.73 | 549.03 ± 4.85 | +15.28% | 39.99 ± 0.04 | 29.43 ± 0.06 | +35.89% |
| 1024 | 624.99 ± 1.68 | 540.42 ± 4.98 | +15.65% | 39.61 ± 0.10 | 29.50 ± 0.08 | +34.28% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
