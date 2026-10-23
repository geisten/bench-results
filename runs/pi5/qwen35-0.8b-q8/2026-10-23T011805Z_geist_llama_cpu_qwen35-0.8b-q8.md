# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `cdc4ba43c58a`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.82 ± 0.40 | 120.86 ± 6.28 | -2.52% | 13.63 ± 0.02 | 11.91 ± 0.29 | +14.46% |
| 256 | 110.73 ± 0.06 | 91.23 ± 2.12 | +21.37% | 13.58 ± 0.05 | 11.60 ± 0.11 | +17.08% |
| 512 | 105.97 ± 0.32 | 86.17 ± 5.53 | +22.98% | 13.50 ± 0.07 | 11.41 ± 0.07 | +18.31% |
| 1024 | 100.80 ± 0.26 | 80.24 ± 0.78 | +25.62% | 13.32 ± 0.04 | 11.09 ± 0.03 | +20.12% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
