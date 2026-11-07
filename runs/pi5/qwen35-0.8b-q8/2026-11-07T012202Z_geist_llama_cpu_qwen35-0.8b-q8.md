# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.62 ± 0.15 | 127.67 ± 3.47 | -7.87% | 13.72 ± 0.05 | 12.13 ± 0.20 | +13.10% |
| 256 | 110.28 ± 0.33 | 103.12 ± 1.07 | +6.95% | 13.70 ± 0.09 | 11.84 ± 0.07 | +15.71% |
| 512 | 105.71 ± 0.10 | 96.87 ± 0.12 | +9.13% | 13.63 ± 0.03 | 11.51 ± 0.07 | +18.39% |
| 1024 | 100.54 ± 0.25 | 94.66 ± 0.44 | +6.21% | 13.38 ± 0.06 | 11.21 ± 0.08 | +19.43% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
