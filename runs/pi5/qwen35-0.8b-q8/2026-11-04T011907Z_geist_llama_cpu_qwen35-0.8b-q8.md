# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.58 ± 0.18 | 128.98 ± 2.07 | -8.84% | 13.70 ± 0.14 | 11.81 ± 0.07 | +15.99% |
| 256 | 110.17 ± 0.33 | 108.68 ± 6.13 | +1.37% | 13.58 ± 0.09 | 11.80 ± 0.05 | +15.10% |
| 512 | 105.67 ± 0.25 | 96.61 ± 0.42 | +9.37% | 13.50 ± 0.09 | 11.66 ± 0.11 | +15.81% |
| 1024 | 100.91 ± 0.20 | 94.98 ± 0.15 | +6.25% | 13.23 ± 0.14 | 11.26 ± 0.10 | +17.50% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
