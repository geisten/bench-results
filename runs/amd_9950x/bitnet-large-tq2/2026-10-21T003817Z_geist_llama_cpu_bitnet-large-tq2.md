# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `24515004c598`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1749.96 ± 25.12 | 1343.91 ± 15.40 | +30.21% | 319.75 ± 2.85 | 239.45 ± 1.10 | +33.53% |
| 256 | 1738.32 ± 13.40 | 1361.22 ± 1.42 | +27.70% | 300.14 ± 1.45 | 212.44 ± 1.51 | +41.29% |
| 512 | 1669.66 ± 15.56 | 1331.28 ± 5.70 | +25.42% | 268.11 ± 3.38 | 184.30 ± 0.78 | +45.47% |
| 1024 | 1540.95 ± 8.58 | 1271.20 ± 8.04 | +21.22% | 217.34 ± 2.40 | 143.19 ± 1.06 | +51.78% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
