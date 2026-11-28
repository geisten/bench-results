# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `0b0ee998e552`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.20 ± 1.60 | 518.99 ± 5.82 | +10.64% | 40.65 ± 0.07 | 28.92 ± 0.13 | +40.53% |
| 256 | 591.15 ± 1.42 | 537.09 ± 5.22 | +10.07% | 40.50 ± 0.08 | 29.45 ± 0.15 | +37.50% |
| 512 | 632.82 ± 1.15 | 549.84 ± 5.24 | +15.09% | 40.13 ± 0.07 | 29.56 ± 0.05 | +35.75% |
| 1024 | 626.89 ± 1.30 | 544.64 ± 6.47 | +15.10% | 39.84 ± 0.06 | 29.28 ± 0.05 | +36.06% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
