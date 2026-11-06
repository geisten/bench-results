# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `406a3c0519ec`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 573.53 ± 1.72 | 513.91 ± 5.24 | +11.60% | 40.53 ± 0.07 | 28.88 ± 0.03 | +40.32% |
| 256 | 589.62 ± 1.29 | 534.35 ± 4.62 | +10.34% | 40.36 ± 0.08 | 28.93 ± 0.07 | +39.49% |
| 512 | 631.75 ± 2.38 | 543.48 ± 5.11 | +16.24% | 39.99 ± 0.06 | 29.62 ± 0.03 | +35.04% |
| 1024 | 623.71 ± 1.12 | 541.95 ± 4.98 | +15.08% | 39.60 ± 0.05 | 29.33 ± 0.07 | +35.01% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
