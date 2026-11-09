# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2555.75 ± 36.32 | 1361.74 ± 5.31 | +87.68% | 327.60 ± 2.79 | 239.01 ± 2.00 | +37.07% |
| 256 | 2544.42 ± 41.38 | 1433.38 ± 5.18 | +77.51% | 309.18 ± 1.41 | 211.92 ± 1.16 | +45.90% |
| 512 | 2359.63 ± 21.01 | 1399.62 ± 4.58 | +68.59% | 275.83 ± 1.07 | 184.76 ± 1.04 | +49.29% |
| 1024 | 2107.16 ± 8.39 | 1336.81 ± 1.90 | +57.63% | 219.99 ± 0.98 | 145.02 ± 1.95 | +51.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
