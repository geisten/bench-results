# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 151.35 ± 0.55 | 102.24 ± 0.37 | +48.03% | 44.58 ± 0.23 | 40.99 ± 0.08 | +8.75% |
| 256 | 144.62 ± 0.65 | 99.40 ± 0.19 | +45.50% | 39.69 ± 0.22 | 30.98 ± 0.04 | +28.12% |
| 512 | 128.89 ± 0.22 | 94.79 ± 0.11 | +35.98% | 32.21 ± 0.46 | 25.41 ± 0.03 | +26.77% |
| 1024 | 85.83 ± 0.12 | 88.51 ± 0.17 | -3.03% | 21.78 ± 0.35 | 17.86 ± 0.02 | +21.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
