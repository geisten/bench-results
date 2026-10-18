# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `c993379b0746`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 576.90 ± 1.53 | 517.18 ± 5.33 | +11.55% | 40.73 ± 0.04 | 29.40 ± 0.03 | +38.53% |
| 256 | 592.98 ± 1.47 | 535.53 ± 5.48 | +10.73% | 40.54 ± 0.07 | 29.39 ± 0.10 | +37.92% |
| 512 | 635.90 ± 1.64 | 547.84 ± 4.94 | +16.08% | 40.13 ± 0.05 | 29.47 ± 0.02 | +36.18% |
| 1024 | 628.17 ± 1.89 | 540.87 ± 4.80 | +16.14% | 39.87 ± 0.15 | 29.63 ± 0.04 | +34.57% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
