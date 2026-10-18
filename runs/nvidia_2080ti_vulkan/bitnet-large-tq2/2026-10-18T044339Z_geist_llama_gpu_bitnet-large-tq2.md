# Current GPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8552.72 ± 64.78 | 8322.39 ± 1380.87 | +2.77% | 349.98 ± 1.80 | 388.36 ± 1.67 | -9.88% |
| 256 | 11023.79 ± 7.36 | 12328.60 ± 988.65 | -10.58% | 349.27 ± 0.66 | 382.00 ± 3.09 | -8.57% |
| 512 | 13236.47 ± 9.92 | 14077.90 ± 72.50 | -5.98% | 341.59 ± 0.60 | 368.80 ± 1.08 | -7.38% |
| 1024 | 11895.08 ± 1.80 | 13155.60 ± 18.30 | -9.58% | 324.32 ± 0.61 | 353.17 ± 1.85 | -8.17% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
