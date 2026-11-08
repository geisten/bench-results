# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 151.09 ± 0.13 | 102.08 ± 0.07 | +48.01% | 41.69 ± 0.14 | 38.85 ± 0.05 | +7.31% |
| 256 | 144.52 ± 0.20 | 98.51 ± 0.27 | +46.71% | 37.57 ± 0.22 | 29.79 ± 0.02 | +26.11% |
| 512 | 128.83 ± 0.19 | 94.22 ± 0.29 | +36.73% | 30.81 ± 0.16 | 24.47 ± 0.03 | +25.93% |
| 1024 | 85.67 ± 0.10 | 88.02 ± 0.15 | -2.67% | 21.76 ± 0.30 | 17.34 ± 0.05 | +25.49% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
