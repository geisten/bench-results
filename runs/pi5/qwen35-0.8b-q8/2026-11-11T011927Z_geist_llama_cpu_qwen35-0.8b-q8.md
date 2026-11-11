# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 116.82 ± 0.24 | 120.67 ± 3.10 | -3.19% | 13.27 ± 0.06 | 11.57 ± 0.17 | +14.65% |
| 256 | 109.51 ± 0.18 | 100.59 ± 0.48 | +8.87% | 13.26 ± 0.03 | 11.58 ± 0.19 | +14.55% |
| 512 | 105.06 ± 0.27 | 92.88 ± 0.23 | +13.11% | 13.14 ± 0.06 | 11.42 ± 0.11 | +15.11% |
| 1024 | 100.02 ± 0.14 | 91.47 ± 0.28 | +9.34% | 12.91 ± 0.14 | 10.98 ± 0.05 | +17.60% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
