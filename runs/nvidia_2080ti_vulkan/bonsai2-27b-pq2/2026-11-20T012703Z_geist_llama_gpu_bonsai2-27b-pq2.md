# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `aeb3a50153d7`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.57 ± 2.15 | 517.27 ± 4.09 | +10.88% | 40.62 ± 0.06 | 29.19 ± 0.11 | +39.15% |
| 256 | 588.01 ± 1.45 | 535.18 ± 4.58 | +9.87% | 40.39 ± 0.07 | 29.33 ± 0.03 | +37.70% |
| 512 | 632.35 ± 0.78 | 548.56 ± 3.87 | +15.28% | 40.09 ± 0.05 | 29.62 ± 0.06 | +35.37% |
| 1024 | 625.22 ± 1.32 | 541.37 ± 5.02 | +15.49% | 39.74 ± 0.10 | 29.36 ± 0.10 | +35.33% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
