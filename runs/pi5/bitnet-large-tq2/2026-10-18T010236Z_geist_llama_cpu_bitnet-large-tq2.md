# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 147.32 ± 0.20 | 103.97 ± 0.09 | +41.69% | 46.17 ± 0.25 | 42.37 ± 0.09 | +8.95% |
| 256 | 140.84 ± 0.09 | 101.04 ± 0.07 | +39.39% | 41.13 ± 0.35 | 31.75 ± 0.05 | +29.54% |
| 512 | 126.09 ± 0.13 | 96.87 ± 0.07 | +30.17% | 32.92 ± 0.58 | 25.93 ± 0.05 | +26.98% |
| 1024 | 84.48 ± 0.10 | 90.49 ± 0.08 | -6.65% | 22.59 ± 0.71 | 18.34 ± 0.04 | +23.20% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
