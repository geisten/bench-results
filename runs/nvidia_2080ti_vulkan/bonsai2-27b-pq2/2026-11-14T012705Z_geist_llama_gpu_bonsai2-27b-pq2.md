# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `666d971e5db2`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.28 ± 2.34 | 515.67 ± 5.25 | +11.75% | 40.55 ± 0.03 | 28.91 ± 0.02 | +40.26% |
| 256 | 591.19 ± 1.77 | 536.01 ± 4.89 | +10.30% | 40.39 ± 0.03 | 28.97 ± 0.06 | +39.42% |
| 512 | 633.51 ± 2.24 | 544.26 ± 4.40 | +16.40% | 40.05 ± 0.05 | 29.73 ± 0.07 | +34.71% |
| 1024 | 626.31 ± 1.84 | 544.17 ± 4.54 | +15.09% | 39.76 ± 0.11 | 29.35 ± 0.12 | +35.44% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
