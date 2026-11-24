# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `acaed04bf0f2`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.15 ± 1.36 | 517.71 ± 5.14 | +11.10% | 40.71 ± 0.05 | 29.23 ± 0.07 | +39.27% |
| 256 | 591.82 ± 1.15 | 536.69 ± 4.92 | +10.27% | 40.52 ± 0.05 | 29.19 ± 0.11 | +38.82% |
| 512 | 633.81 ± 1.34 | 549.71 ± 4.32 | +15.30% | 40.15 ± 0.05 | 29.52 ± 0.07 | +36.03% |
| 1024 | 627.31 ± 1.18 | 545.91 ± 4.81 | +14.91% | 39.87 ± 0.14 | 29.40 ± 0.09 | +35.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
