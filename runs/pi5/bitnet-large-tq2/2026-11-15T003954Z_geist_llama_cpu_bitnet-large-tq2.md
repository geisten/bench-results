# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 152.37 ± 0.31 | 102.82 ± 0.13 | +48.20% | 44.79 ± 0.04 | 41.16 ± 0.10 | +8.80% |
| 256 | 145.50 ± 0.30 | 99.91 ± 0.16 | +45.63% | 39.65 ± 0.20 | 31.08 ± 0.05 | +27.57% |
| 512 | 129.75 ± 0.32 | 95.61 ± 0.15 | +35.71% | 31.16 ± 0.10 | 25.43 ± 0.03 | +22.54% |
| 1024 | 86.06 ± 0.16 | 89.24 ± 0.18 | -3.57% | 21.67 ± 0.06 | 17.86 ± 0.03 | +21.32% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
