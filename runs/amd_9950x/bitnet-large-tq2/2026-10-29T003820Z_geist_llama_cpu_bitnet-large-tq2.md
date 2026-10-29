# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `c212773b0268`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2571.32 ± 17.47 | 1363.82 ± 4.18 | +88.54% | 321.35 ± 1.40 | 235.86 ± 4.85 | +36.25% |
| 256 | 2522.04 ± 25.32 | 1426.41 ± 3.48 | +76.81% | 303.48 ± 1.53 | 217.56 ± 1.42 | +39.50% |
| 512 | 2362.18 ± 15.33 | 1395.13 ± 5.85 | +69.32% | 272.67 ± 2.44 | 187.11 ± 1.18 | +45.73% |
| 1024 | 2110.87 ± 13.06 | 1338.42 ± 1.92 | +57.71% | 217.39 ± 4.48 | 146.09 ± 1.51 | +48.81% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
