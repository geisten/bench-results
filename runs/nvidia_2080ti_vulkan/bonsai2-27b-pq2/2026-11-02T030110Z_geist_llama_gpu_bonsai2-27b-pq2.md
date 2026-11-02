# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `f83e03b37679`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.52 ± 2.09 | 516.13 ± 5.10 | +11.31% | 40.55 ± 0.10 | 29.35 ± 0.08 | +38.16% |
| 256 | 587.96 ± 1.28 | 536.08 ± 5.16 | +9.68% | 40.26 ± 0.07 | 29.60 ± 0.08 | +36.01% |
| 512 | 632.96 ± 1.11 | 549.37 ± 5.78 | +15.22% | 40.01 ± 0.06 | 29.63 ± 0.13 | +35.01% |
| 1024 | 624.49 ± 0.88 | 542.27 ± 3.27 | +15.16% | 39.62 ± 0.07 | 29.67 ± 0.07 | +33.51% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
