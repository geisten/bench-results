# Current GPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `1515c60147c9`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8402.39 ± 214.53 | 8315.82 ± 1331.38 | +1.04% | 349.69 ± 1.68 | 387.54 ± 2.10 | -9.77% |
| 256 | 11020.23 ± 8.78 | 11374.10 ± 1943.26 | -3.11% | 348.86 ± 0.49 | 377.78 ± 2.87 | -7.65% |
| 512 | 13223.48 ± 21.31 | 14190.70 ± 79.75 | -6.82% | 341.94 ± 0.51 | 366.98 ± 1.50 | -6.82% |
| 1024 | 11878.52 ± 4.06 | 13230.25 ± 33.00 | -10.22% | 325.12 ± 0.62 | 351.01 ± 2.75 | -7.38% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
