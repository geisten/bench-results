# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `50863de30fe7`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.35 ± 1.79 | 516.36 ± 5.21 | +11.23% | 40.51 ± 0.03 | 29.15 ± 0.03 | +38.95% |
| 256 | 589.38 ± 1.67 | 535.73 ± 4.90 | +10.01% | 40.35 ± 0.09 | 29.32 ± 0.10 | +37.64% |
| 512 | 631.66 ± 1.77 | 547.95 ± 5.17 | +15.28% | 40.02 ± 0.07 | 29.28 ± 0.13 | +36.66% |
| 1024 | 624.11 ± 1.60 | 543.39 ± 4.99 | +14.85% | 39.63 ± 0.11 | 29.50 ± 0.08 | +34.33% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
