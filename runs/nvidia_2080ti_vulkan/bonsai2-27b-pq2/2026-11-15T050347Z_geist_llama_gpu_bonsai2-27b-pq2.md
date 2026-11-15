# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `7765b16fc97f`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 575.21 ± 2.11 | 515.30 ± 5.08 | +11.63% | 40.57 ± 0.07 | 28.91 ± 0.07 | +40.32% |
| 256 | 589.04 ± 2.27 | 534.69 ± 4.61 | +10.16% | 40.27 ± 0.06 | 28.89 ± 0.05 | +39.38% |
| 512 | 632.91 ± 1.31 | 545.53 ± 3.89 | +16.02% | 39.98 ± 0.05 | 29.69 ± 0.06 | +34.65% |
| 1024 | 625.38 ± 1.55 | 544.16 ± 4.61 | +14.93% | 39.63 ± 0.09 | 29.31 ± 0.10 | +35.24% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
