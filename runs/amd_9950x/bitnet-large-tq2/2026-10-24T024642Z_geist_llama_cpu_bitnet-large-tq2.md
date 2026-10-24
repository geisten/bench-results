# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `14ac9f78e1df`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2507.52 ± 50.34 | 1357.08 ± 4.36 | +84.77% | 324.69 ± 2.07 | 240.09 ± 2.97 | +35.24% |
| 256 | 2481.49 ± 14.71 | 1404.94 ± 9.55 | +76.63% | 306.62 ± 1.82 | 212.76 ± 1.26 | +44.12% |
| 512 | 2352.50 ± 14.00 | 1388.02 ± 6.90 | +69.49% | 273.42 ± 5.02 | 183.31 ± 1.44 | +49.15% |
| 1024 | 2122.47 ± 14.41 | 1327.41 ± 1.23 | +59.90% | 216.58 ± 3.60 | 143.48 ± 1.40 | +50.94% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
