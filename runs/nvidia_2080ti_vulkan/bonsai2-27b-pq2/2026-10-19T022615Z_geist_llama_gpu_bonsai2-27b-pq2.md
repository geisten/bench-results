# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `2b5263f87833`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.12 ± 1.86 | 516.43 ± 4.98 | +11.56% | 40.62 ± 0.06 | 29.19 ± 0.08 | +39.16% |
| 256 | 592.77 ± 2.43 | 535.39 ± 4.82 | +10.72% | 40.48 ± 0.06 | 29.11 ± 0.10 | +39.06% |
| 512 | 635.69 ± 1.59 | 548.83 ± 4.97 | +15.83% | 40.06 ± 0.04 | 29.54 ± 0.07 | +35.61% |
| 1024 | 628.10 ± 1.53 | 542.65 ± 5.24 | +15.75% | 39.78 ± 0.10 | 29.64 ± 0.07 | +34.23% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
