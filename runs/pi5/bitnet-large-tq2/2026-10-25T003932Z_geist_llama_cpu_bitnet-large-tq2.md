# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 151.65 ± 0.21 | 103.38 ± 0.10 | +46.68% | 44.06 ± 0.12 | 40.88 ± 0.15 | +7.77% |
| 256 | 145.04 ± 0.11 | 99.80 ± 0.56 | +45.33% | 39.71 ± 0.18 | 30.75 ± 0.04 | +29.13% |
| 512 | 129.35 ± 0.13 | 94.81 ± 0.14 | +36.42% | 32.36 ± 0.15 | 25.23 ± 0.10 | +28.29% |
| 1024 | 85.75 ± 0.22 | 88.77 ± 0.21 | -3.40% | 22.82 ± 0.35 | 17.84 ± 0.05 | +27.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
