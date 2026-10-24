# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `14ac9f78e1df`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.50 ± 1.68 | 513.57 ± 5.59 | +11.67% | 40.50 ± 0.04 | 28.91 ± 0.04 | +40.07% |
| 256 | 589.04 ± 0.61 | 534.07 ± 4.91 | +10.29% | 40.35 ± 0.14 | 28.98 ± 0.08 | +39.22% |
| 512 | 633.74 ± 1.71 | 545.49 ± 3.53 | +16.18% | 40.01 ± 0.06 | 29.41 ± 0.08 | +36.04% |
| 1024 | 625.50 ± 1.84 | 543.05 ± 5.14 | +15.18% | 39.64 ± 0.15 | 29.27 ± 0.09 | +35.41% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
