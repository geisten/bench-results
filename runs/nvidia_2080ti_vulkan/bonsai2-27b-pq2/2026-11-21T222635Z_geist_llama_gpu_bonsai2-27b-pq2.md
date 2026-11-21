# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `aeb3a50153d7`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.58 ± 1.68 | 517.78 ± 4.93 | +10.97% | 40.67 ± 0.21 | 28.60 ± 0.55 | +42.18% |
| 256 | 590.57 ± 1.77 | 536.59 ± 5.21 | +10.06% | 40.49 ± 0.09 | 29.02 ± 0.03 | +39.54% |
| 512 | 633.31 ± 2.42 | 548.29 ± 5.43 | +15.51% | 40.16 ± 0.12 | 29.58 ± 0.06 | +35.80% |
| 1024 | 624.83 ± 1.55 | 542.89 ± 6.39 | +15.09% | 39.79 ± 0.11 | 29.48 ± 0.10 | +34.96% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
