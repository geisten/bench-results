# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `db8314e2a3a3`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 577.07 ± 3.01 | 518.13 ± 4.58 | +11.38% | 40.53 ± 0.05 | 29.02 ± 0.07 | +39.68% |
| 256 | 592.11 ± 1.38 | 535.85 ± 4.98 | +10.50% | 40.40 ± 0.08 | 29.20 ± 0.10 | +38.38% |
| 512 | 635.04 ± 1.15 | 548.24 ± 4.10 | +15.83% | 40.02 ± 0.04 | 29.55 ± 0.24 | +35.41% |
| 1024 | 627.54 ± 1.68 | 540.13 ± 4.54 | +16.18% | 39.75 ± 0.14 | 29.43 ± 0.06 | +35.07% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
