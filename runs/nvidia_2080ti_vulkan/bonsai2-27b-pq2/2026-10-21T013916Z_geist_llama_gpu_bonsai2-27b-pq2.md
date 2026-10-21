# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `24515004c598`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 580.15 ± 2.30 | 518.71 ± 6.22 | +11.84% | 40.90 ± 0.15 | 29.31 ± 0.08 | +39.55% |
| 256 | 595.95 ± 4.10 | 537.58 ± 6.49 | +10.86% | 40.68 ± 0.15 | 29.51 ± 0.04 | +37.88% |
| 512 | 641.15 ± 4.21 | 550.70 ± 6.19 | +16.42% | 40.39 ± 0.16 | 29.74 ± 0.03 | +35.78% |
| 1024 | 633.39 ± 3.65 | 544.12 ± 5.46 | +16.40% | 40.04 ± 0.18 | 29.29 ± 0.08 | +36.71% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
