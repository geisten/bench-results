# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2522.55 ± 41.42 | 1359.85 ± 2.70 | +85.50% | 326.38 ± 1.54 | 237.62 ± 2.18 | +37.35% |
| 256 | 2469.16 ± 52.61 | 1381.75 ± 10.58 | +78.70% | 308.74 ± 1.57 | 210.57 ± 1.45 | +46.62% |
| 512 | 2327.05 ± 23.83 | 1376.01 ± 7.28 | +69.12% | 276.63 ± 2.43 | 180.20 ± 1.22 | +53.52% |
| 1024 | 2070.06 ± 9.59 | 1323.67 ± 4.39 | +56.39% | 217.12 ± 3.78 | 142.64 ± 1.04 | +52.22% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
