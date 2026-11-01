# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 150.88 ± 0.73 | 102.47 ± 0.16 | +47.25% | 41.63 ± 0.09 | 38.66 ± 0.13 | +7.68% |
| 256 | 143.90 ± 0.55 | 99.28 ± 0.15 | +44.94% | 37.35 ± 0.21 | 29.68 ± 0.05 | +25.85% |
| 512 | 128.84 ± 0.53 | 94.71 ± 0.10 | +36.03% | 30.69 ± 0.22 | 24.43 ± 0.06 | +25.63% |
| 1024 | 85.87 ± 0.28 | 88.71 ± 0.14 | -3.19% | 21.81 ± 0.34 | 17.32 ± 0.10 | +25.94% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
