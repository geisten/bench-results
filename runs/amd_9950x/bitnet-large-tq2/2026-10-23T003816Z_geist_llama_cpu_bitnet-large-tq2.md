# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `cdc4ba43c58a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2576.79 ± 41.15 | 1359.67 ± 3.19 | +89.52% | 325.43 ± 2.96 | 232.90 ± 4.12 | +39.73% |
| 256 | 2521.56 ± 36.03 | 1407.41 ± 6.38 | +79.16% | 307.26 ± 1.50 | 212.95 ± 1.61 | +44.29% |
| 512 | 2347.01 ± 21.75 | 1385.65 ± 4.66 | +69.38% | 273.83 ± 1.62 | 183.89 ± 2.27 | +48.91% |
| 1024 | 2093.28 ± 18.15 | 1329.91 ± 3.25 | +57.40% | 220.60 ± 2.82 | 142.20 ± 2.43 | +55.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
