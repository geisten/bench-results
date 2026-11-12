# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `48a84627b0c5`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.58 ± 2.25 | 514.03 ± 6.53 | +11.59% | 40.51 ± 0.03 | 28.90 ± 0.04 | +40.18% |
| 256 | 590.66 ± 1.89 | 534.40 ± 4.33 | +10.53% | 40.35 ± 0.10 | 28.91 ± 0.10 | +39.56% |
| 512 | 632.32 ± 1.27 | 543.86 ± 5.82 | +16.26% | 39.99 ± 0.04 | 29.67 ± 0.10 | +34.80% |
| 1024 | 624.75 ± 1.41 | 542.91 ± 5.47 | +15.07% | 39.67 ± 0.10 | 29.26 ± 0.10 | +35.55% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
