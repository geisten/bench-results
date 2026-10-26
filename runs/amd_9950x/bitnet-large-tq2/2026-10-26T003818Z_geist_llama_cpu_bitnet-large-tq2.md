# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `eedaae6cae7b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2615.13 ± 17.57 | 1364.80 ± 11.13 | +91.61% | 332.04 ± 3.00 | 245.38 ± 3.88 | +35.32% |
| 256 | 2557.18 ± 29.00 | 1431.63 ± 5.20 | +78.62% | 310.87 ± 1.46 | 215.50 ± 3.03 | +44.26% |
| 512 | 2377.73 ± 20.61 | 1401.88 ± 5.29 | +69.61% | 281.43 ± 2.76 | 183.96 ± 1.71 | +52.99% |
| 1024 | 2117.30 ± 22.01 | 1339.53 ± 2.49 | +58.06% | 222.81 ± 3.83 | 143.95 ± 1.66 | +54.78% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
