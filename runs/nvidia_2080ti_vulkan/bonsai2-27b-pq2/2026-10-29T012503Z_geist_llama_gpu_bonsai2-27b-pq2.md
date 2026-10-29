# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `c212773b0268`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.27 ± 2.71 | 519.57 ± 5.18 | +10.53% | 40.53 ± 0.08 | 29.00 ± 0.02 | +39.76% |
| 256 | 589.43 ± 0.86 | 536.28 ± 5.57 | +9.91% | 40.35 ± 0.06 | 29.12 ± 0.04 | +38.55% |
| 512 | 633.18 ± 2.96 | 548.12 ± 4.51 | +15.52% | 39.98 ± 0.08 | 29.61 ± 0.04 | +35.04% |
| 1024 | 623.49 ± 0.94 | 542.75 ± 4.94 | +14.88% | 39.60 ± 0.06 | 29.32 ± 0.03 | +35.09% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
