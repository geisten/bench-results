# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `fda9c7a98c7b`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 56.93 ± 0.08 | 128.21 ± 2.74 | -55.60% | 13.85 ± 0.06 | 11.92 ± 0.07 | +16.26% |
| 256 | 55.39 ± 0.12 | 108.85 ± 5.65 | -49.12% | 13.94 ± 0.04 | 11.88 ± 0.03 | +17.31% |
| 512 | 54.30 ± 0.14 | 102.07 ± 6.96 | -46.80% | 13.81 ± 0.03 | 11.67 ± 0.03 | +18.37% |
| 1024 | 53.00 ± 0.05 | 95.32 ± 6.79 | -44.39% | 13.59 ± 0.06 | 11.39 ± 0.04 | +19.26% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
