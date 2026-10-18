# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2385.10 ± 20.82 | 1363.03 ± 7.10 | +74.99% | 325.19 ± 4.59 | 244.29 ± 2.98 | +33.12% |
| 256 | 2362.97 ± 25.55 | 1410.76 ± 15.47 | +67.50% | 308.46 ± 3.50 | 213.74 ± 1.43 | +44.31% |
| 512 | 2225.94 ± 11.78 | 1389.68 ± 2.96 | +60.18% | 275.71 ± 1.91 | 184.95 ± 1.43 | +49.07% |
| 1024 | 2011.48 ± 8.57 | 1334.92 ± 3.37 | +50.68% | 219.13 ± 2.39 | 143.71 ± 1.60 | +52.48% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
