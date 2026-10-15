# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `ebcdfb017ba6`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.80 ± 1.52 | 519.48 ± 4.88 | +10.84% | 40.68 ± 0.14 | 29.07 ± 0.17 | +39.92% |
| 256 | 592.09 ± 2.07 | 532.08 ± 1.50 | +11.28% | 40.39 ± 0.07 | 29.21 ± 0.15 | +38.29% |
| 512 | 635.43 ± 1.55 | 548.99 ± 5.01 | +15.74% | 40.15 ± 0.12 | 29.34 ± 0.06 | +36.84% |
| 1024 | 626.55 ± 1.27 | 537.98 ± 5.14 | +16.46% | 39.71 ± 0.13 | 29.33 ± 0.11 | +35.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
