# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2578.24 ± 51.26 | 1361.59 ± 5.09 | +89.36% | 324.22 ± 4.07 | 247.84 ± 2.25 | +30.82% |
| 256 | 2570.60 ± 31.41 | 1421.96 ± 4.99 | +80.78% | 307.50 ± 2.57 | 222.97 ± 2.37 | +37.91% |
| 512 | 2366.01 ± 14.87 | 1400.63 ± 5.56 | +68.92% | 273.95 ± 6.26 | 191.54 ± 1.64 | +43.02% |
| 1024 | 2114.44 ± 7.53 | 1339.44 ± 3.11 | +57.86% | 219.09 ± 4.56 | 147.06 ± 1.03 | +48.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
