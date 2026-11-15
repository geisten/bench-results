# Current GPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8589.45 ± 43.74 | 8328.76 ± 1423.09 | +3.13% | 353.93 ± 1.26 | 388.42 ± 2.16 | -8.88% |
| 256 | 11027.59 ± 3.32 | 12943.80 ± 166.95 | -14.80% | 351.28 ± 0.27 | 384.00 ± 4.01 | -8.52% |
| 512 | 13249.83 ± 7.89 | 14143.80 ± 35.20 | -6.32% | 343.57 ± 0.21 | 372.24 ± 2.83 | -7.70% |
| 1024 | 11906.15 ± 7.48 | 13185.35 ± 22.90 | -9.70% | 326.46 ± 0.20 | 357.17 ± 2.70 | -8.60% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
