# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `aeb3a50153d7`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.31 ± 1.86 | 518.77 ± 6.11 | +10.90% | 40.59 ± 0.09 | 28.73 ± 0.09 | +41.28% |
| 256 | 589.87 ± 1.99 | 535.98 ± 4.49 | +10.05% | 40.36 ± 0.10 | 29.39 ± 0.09 | +37.34% |
| 512 | 632.75 ± 1.20 | 547.80 ± 5.19 | +15.51% | 40.04 ± 0.03 | 29.64 ± 0.08 | +35.08% |
| 1024 | 625.03 ± 1.86 | 544.34 ± 5.69 | +14.82% | 39.71 ± 0.10 | 29.44 ± 0.08 | +34.86% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
