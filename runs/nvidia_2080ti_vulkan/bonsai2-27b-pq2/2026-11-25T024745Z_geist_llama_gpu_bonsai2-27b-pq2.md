# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `d231cb8104bc`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.92 ± 1.53 | 517.01 ± 4.78 | +11.20% | 40.80 ± 0.09 | 29.23 ± 0.05 | +39.56% |
| 256 | 590.73 ± 2.52 | 537.10 ± 4.35 | +9.99% | 40.54 ± 0.11 | 29.16 ± 0.10 | +39.01% |
| 512 | 634.69 ± 1.43 | 550.44 ± 5.18 | +15.31% | 40.27 ± 0.13 | 29.56 ± 0.05 | +36.22% |
| 1024 | 625.14 ± 1.47 | 545.31 ± 4.62 | +14.64% | 39.82 ± 0.10 | 29.37 ± 0.07 | +35.59% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
