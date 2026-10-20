# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `44479afd263d`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.93 ± 1.80 | 516.56 ± 4.33 | +11.69% | 40.60 ± 0.09 | 29.18 ± 0.12 | +39.12% |
| 256 | 592.02 ± 1.85 | 535.63 ± 4.39 | +10.53% | 40.47 ± 0.05 | 29.48 ± 0.11 | +37.30% |
| 512 | 635.38 ± 1.98 | 549.01 ± 5.51 | +15.73% | 40.08 ± 0.06 | 29.43 ± 0.09 | +36.16% |
| 1024 | 627.75 ± 1.32 | 542.05 ± 4.40 | +15.81% | 39.80 ± 0.11 | 29.40 ± 0.09 | +35.38% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
