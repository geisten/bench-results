# Current GPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8556.72 ± 51.51 | 8352.05 ± 1379.41 | +2.45% | 349.25 ± 1.49 | 389.13 ± 2.52 | -10.25% |
| 256 | 11004.13 ± 5.20 | 12920.60 ± 457.50 | -14.83% | 349.05 ± 1.63 | 382.04 ± 2.48 | -8.64% |
| 512 | 13267.17 ± 4.47 | 14115.20 ± 82.90 | -6.01% | 340.94 ± 0.50 | 372.62 ± 2.19 | -8.50% |
| 1024 | 11916.19 ± 9.58 | 13221.00 ± 54.20 | -9.87% | 323.20 ± 0.82 | 354.91 ± 3.52 | -8.93% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
