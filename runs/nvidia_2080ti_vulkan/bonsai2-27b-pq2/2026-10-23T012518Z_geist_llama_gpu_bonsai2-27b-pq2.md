# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `cdc4ba43c58a`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.95 ± 2.26 | 513.39 ± 5.46 | +11.80% | 40.44 ± 0.02 | 29.10 ± 0.03 | +38.96% |
| 256 | 589.53 ± 0.57 | 533.37 ± 4.85 | +10.53% | 40.33 ± 0.10 | 29.41 ± 0.07 | +37.11% |
| 512 | 633.84 ± 1.40 | 545.98 ± 4.93 | +16.09% | 39.98 ± 0.03 | 29.35 ± 0.08 | +36.22% |
| 1024 | 625.32 ± 2.16 | 539.28 ± 4.40 | +15.95% | 39.66 ± 0.16 | 29.41 ± 0.07 | +34.84% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
