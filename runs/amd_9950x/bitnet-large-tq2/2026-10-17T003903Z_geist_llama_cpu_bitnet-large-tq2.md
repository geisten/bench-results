# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `0b892b0f366c`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1780.90 ± 36.90 | 1346.08 ± 6.20 | +32.30% | 321.35 ± 3.36 | 232.88 ± 2.93 | +37.99% |
| 256 | 1736.24 ± 31.98 | 1360.42 ± 2.29 | +27.62% | 304.06 ± 1.26 | 206.91 ± 1.17 | +46.96% |
| 512 | 1691.11 ± 22.65 | 1323.40 ± 4.33 | +27.78% | 273.80 ± 2.10 | 179.68 ± 2.64 | +52.38% |
| 1024 | 1565.22 ± 24.59 | 1267.39 ± 5.00 | +23.50% | 220.83 ± 0.72 | 141.79 ± 2.12 | +55.75% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
