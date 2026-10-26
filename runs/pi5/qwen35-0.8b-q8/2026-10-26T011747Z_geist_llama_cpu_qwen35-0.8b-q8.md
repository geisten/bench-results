# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `eedaae6cae7b`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.45 ± 0.41 | 125.65 ± 0.77 | -6.52% | 13.65 ± 0.09 | 12.07 ± 0.09 | +13.17% |
| 256 | 110.45 ± 0.35 | 101.41 ± 0.38 | +8.92% | 13.54 ± 0.12 | 11.75 ± 0.15 | +15.21% |
| 512 | 105.63 ± 0.34 | 94.70 ± 0.16 | +11.54% | 13.53 ± 0.10 | 11.46 ± 0.12 | +18.02% |
| 1024 | 100.89 ± 0.19 | 92.79 ± 0.17 | +8.73% | 13.14 ± 0.12 | 11.15 ± 0.08 | +17.83% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
