# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `f19377734f16`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.74 ± 2.52 | 517.38 ± 6.01 | +10.89% | 40.46 ± 0.05 | 28.83 ± 0.18 | +40.36% |
| 256 | 589.66 ± 1.11 | 533.43 ± 4.93 | +10.54% | 40.32 ± 0.08 | 29.03 ± 0.07 | +38.89% |
| 512 | 633.47 ± 2.70 | 547.13 ± 4.80 | +15.78% | 39.94 ± 0.07 | 29.38 ± 0.02 | +35.94% |
| 1024 | 625.93 ± 1.72 | 542.06 ± 5.12 | +15.47% | 39.63 ± 0.16 | 29.31 ± 0.18 | +35.19% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
