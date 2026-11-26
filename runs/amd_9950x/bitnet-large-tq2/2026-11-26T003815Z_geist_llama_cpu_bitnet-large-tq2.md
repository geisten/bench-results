# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2523.94 ± 74.73 | 1358.51 ± 6.95 | +85.79% | 327.46 ± 1.70 | 240.48 ± 2.72 | +36.17% |
| 256 | 2557.03 ± 23.91 | 1409.30 ± 7.58 | +81.44% | 307.46 ± 3.35 | 201.39 ± 7.08 | +52.67% |
| 512 | 2356.47 ± 21.88 | 1376.07 ± 7.06 | +71.25% | 273.41 ± 6.39 | 169.94 ± 4.62 | +60.89% |
| 1024 | 2088.97 ± 21.00 | 1327.68 ± 2.18 | +57.34% | 212.81 ± 2.23 | 126.01 ± 3.95 | +68.89% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
