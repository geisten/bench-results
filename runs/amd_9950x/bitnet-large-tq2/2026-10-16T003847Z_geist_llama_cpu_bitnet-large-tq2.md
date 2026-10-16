# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `fda9c7a98c7b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1746.02 ± 18.83 | 1347.62 ± 3.66 | +29.56% | 324.37 ± 2.65 | 240.44 ± 0.87 | +34.90% |
| 256 | 1728.03 ± 23.65 | 1361.03 ± 2.35 | +26.97% | 306.92 ± 2.08 | 211.48 ± 0.85 | +45.13% |
| 512 | 1683.08 ± 15.31 | 1330.36 ± 4.15 | +26.51% | 278.21 ± 2.01 | 181.50 ± 1.23 | +53.28% |
| 1024 | 1553.76 ± 11.14 | 1270.16 ± 3.50 | +22.33% | 228.05 ± 1.24 | 143.16 ± 0.62 | +59.30% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
