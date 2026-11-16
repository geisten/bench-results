# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `99e847f1c898`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.56 ± 1.86 | 516.08 ± 5.65 | +11.33% | 40.58 ± 0.05 | 29.33 ± 0.04 | +38.38% |
| 256 | 590.53 ± 0.61 | 536.72 ± 5.05 | +10.03% | 40.41 ± 0.01 | 29.03 ± 0.05 | +39.22% |
| 512 | 632.64 ± 2.50 | 547.79 ± 3.69 | +15.49% | 40.07 ± 0.04 | 29.85 ± 0.06 | +34.21% |
| 1024 | 625.27 ± 1.09 | 543.70 ± 4.76 | +15.00% | 39.79 ± 0.12 | 29.48 ± 0.12 | +34.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
