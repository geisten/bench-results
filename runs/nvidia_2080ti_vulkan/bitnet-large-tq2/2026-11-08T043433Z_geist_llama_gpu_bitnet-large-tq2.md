# Current GPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8563.31 ± 66.22 | 8328.90 ± 1388.83 | +2.81% | 349.47 ± 2.48 | 387.27 ± 1.54 | -9.76% |
| 256 | 11037.58 ± 5.71 | 12763.10 ± 547.75 | -13.52% | 350.10 ± 1.09 | 380.87 ± 3.35 | -8.08% |
| 512 | 13283.00 ± 4.83 | 14110.65 ± 31.90 | -5.87% | 342.40 ± 1.27 | 369.48 ± 1.14 | -7.33% |
| 1024 | 11935.08 ± 6.82 | 13211.00 ± 42.90 | -9.66% | 325.23 ± 1.14 | 353.46 ± 3.37 | -7.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
