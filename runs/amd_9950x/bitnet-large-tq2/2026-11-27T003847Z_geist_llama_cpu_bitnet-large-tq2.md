# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2540.50 ± 62.19 | 1350.84 ± 14.82 | +88.07% | 323.58 ± 3.98 | 244.77 ± 5.70 | +32.20% |
| 256 | 2515.50 ± 39.99 | 1375.63 ± 15.54 | +82.86% | 306.79 ± 3.43 | 214.96 ± 3.82 | +42.72% |
| 512 | 2306.78 ± 63.90 | 1334.53 ± 17.44 | +72.85% | 266.86 ± 7.94 | 182.65 ± 3.68 | +46.10% |
| 1024 | 1599.16 ± 42.44 | 1309.29 ± 17.13 | +22.14% | 206.27 ± 5.54 | 141.80 ± 1.03 | +45.47% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
