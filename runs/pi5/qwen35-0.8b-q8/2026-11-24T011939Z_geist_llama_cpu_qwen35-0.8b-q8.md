# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.35 ± 0.55 | 121.88 ± 3.62 | -3.71% | 13.45 ± 0.06 | 11.54 ± 0.20 | +16.51% |
| 256 | 109.70 ± 0.74 | 103.23 ± 4.99 | +6.26% | 13.41 ± 0.11 | 11.77 ± 0.20 | +13.96% |
| 512 | 105.42 ± 0.31 | 81.92 ± 0.64 | +28.68% | 13.40 ± 0.06 | 11.24 ± 0.09 | +19.21% |
| 1024 | 100.62 ± 0.15 | 85.60 ± 5.29 | +17.55% | 13.13 ± 0.07 | 10.89 ± 0.04 | +20.49% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
