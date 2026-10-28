# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `13921becb240`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.58 ± 1.58 | 515.90 ± 4.69 | +11.37% | 40.51 ± 0.05 | 29.18 ± 0.04 | +38.83% |
| 256 | 587.84 ± 1.09 | 535.85 ± 4.81 | +9.70% | 40.27 ± 0.07 | 28.90 ± 0.05 | +39.37% |
| 512 | 633.30 ± 1.31 | 547.44 ± 4.35 | +15.68% | 39.98 ± 0.03 | 29.43 ± 0.07 | +35.87% |
| 1024 | 625.00 ± 1.28 | 545.02 ± 5.12 | +14.67% | 39.63 ± 0.08 | 29.46 ± 0.06 | +34.52% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
