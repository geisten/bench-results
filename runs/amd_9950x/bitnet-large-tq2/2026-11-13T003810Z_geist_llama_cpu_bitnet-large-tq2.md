# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2565.31 ± 38.48 | 1361.19 ± 2.20 | +88.46% | 327.23 ± 2.18 | 244.72 ± 1.57 | +33.72% |
| 256 | 2545.45 ± 25.31 | 1417.47 ± 12.14 | +79.58% | 309.31 ± 2.01 | 220.68 ± 1.40 | +40.16% |
| 512 | 2374.97 ± 26.09 | 1394.45 ± 8.35 | +70.32% | 277.25 ± 1.27 | 189.13 ± 1.49 | +46.59% |
| 1024 | 2107.66 ± 22.32 | 1337.61 ± 2.85 | +57.57% | 219.41 ± 2.96 | 146.28 ± 1.29 | +50.00% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
