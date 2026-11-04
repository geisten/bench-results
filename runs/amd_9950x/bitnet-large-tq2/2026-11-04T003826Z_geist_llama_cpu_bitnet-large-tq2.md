# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2577.92 ± 32.88 | 1363.55 ± 5.88 | +89.06% | 326.34 ± 3.53 | 246.08 ± 3.24 | +32.61% |
| 256 | 2571.92 ± 38.77 | 1428.83 ± 7.13 | +80.00% | 307.89 ± 2.23 | 220.73 ± 0.85 | +39.49% |
| 512 | 2395.50 ± 15.35 | 1394.64 ± 6.07 | +71.76% | 273.36 ± 6.54 | 187.92 ± 1.21 | +45.47% |
| 1024 | 2109.94 ± 19.94 | 1337.67 ± 2.63 | +57.73% | 219.31 ± 4.64 | 146.50 ± 1.22 | +49.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
