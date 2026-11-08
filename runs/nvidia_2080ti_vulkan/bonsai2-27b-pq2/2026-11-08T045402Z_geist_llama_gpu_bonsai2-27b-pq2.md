# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `ff31d42364e1`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.42 ± 1.91 | 514.59 ± 6.29 | +11.63% | 40.56 ± 0.09 | 28.91 ± 0.08 | +40.31% |
| 256 | 588.70 ± 0.65 | 535.75 ± 5.96 | +9.88% | 40.35 ± 0.06 | 28.93 ± 0.10 | +39.46% |
| 512 | 632.34 ± 1.83 | 542.99 ± 4.81 | +16.46% | 40.02 ± 0.09 | 29.65 ± 0.02 | +34.98% |
| 1024 | 624.23 ± 1.05 | 543.29 ± 4.75 | +14.90% | 39.67 ± 0.09 | 29.36 ± 0.03 | +35.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
