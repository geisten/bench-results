# Current GPU head-to-head: geist vs llama.cpp

Model: `Ternary-Bonsai-2-27B-PQ2_0.gguf` (`3907dc1658db1f78a9826bf8d5bcb8dc65db0d466388937af57f2294fae62ec1`)

geist `495156f8079f`; llama.cpp `adfffbe41b2c`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 574.65 ± 2.74 | 514.77 ± 5.33 | +11.63% | 40.55 ± 0.02 | 28.99 ± 0.05 | +39.86% |
| 256 | 589.94 ± 1.55 | 534.75 ± 4.81 | +10.32% | 40.38 ± 0.11 | 29.02 ± 0.10 | +39.14% |
| 512 | 633.07 ± 1.45 | 543.33 ± 5.10 | +16.52% | 40.03 ± 0.04 | 29.78 ± 0.05 | +34.44% |
| 1024 | 624.37 ± 1.42 | 542.50 ± 4.59 | +15.09% | 39.69 ± 0.13 | 29.41 ± 0.08 | +34.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
