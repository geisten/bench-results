# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2571.62 ± 28.81 | 1366.90 ± 5.91 | +88.14% | 332.71 ± 2.33 | 244.71 ± 2.00 | +35.96% |
| 256 | 2561.03 ± 46.40 | 1430.13 ± 14.84 | +79.08% | 313.07 ± 3.07 | 221.18 ± 1.17 | +41.55% |
| 512 | 2371.72 ± 8.30 | 1396.32 ± 7.98 | +69.86% | 281.81 ± 1.45 | 189.98 ± 1.28 | +48.34% |
| 1024 | 2112.50 ± 13.14 | 1335.99 ± 2.38 | +58.12% | 225.34 ± 1.42 | 146.42 ± 1.33 | +53.90% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
