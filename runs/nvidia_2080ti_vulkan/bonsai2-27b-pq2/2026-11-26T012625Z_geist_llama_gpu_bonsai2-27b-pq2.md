# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `002ea9d90274`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.53 ± 2.37 | 517.97 ± 5.75 | +11.30% | 40.68 ± 0.04 | 29.18 ± 0.08 | +39.43% |
| 256 | 591.50 ± 0.88 | 536.42 ± 4.79 | +10.27% | 40.53 ± 0.03 | 29.22 ± 0.10 | +38.68% |
| 512 | 633.71 ± 1.36 | 550.47 ± 4.55 | +15.12% | 40.18 ± 0.07 | 29.55 ± 0.07 | +35.96% |
| 1024 | 627.03 ± 1.03 | 546.80 ± 4.15 | +14.67% | 39.88 ± 0.03 | 29.46 ± 0.07 | +35.35% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
