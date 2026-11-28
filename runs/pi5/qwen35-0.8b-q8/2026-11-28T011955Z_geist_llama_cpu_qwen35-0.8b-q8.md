# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a7a01a052466`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 116.04 ± 1.48 | 112.67 ± 0.75 | +2.99% | 13.51 ± 0.05 | 11.31 ± 0.20 | +19.46% |
| 256 | 109.80 ± 0.67 | 82.82 ± 6.32 | +32.58% | 13.51 ± 0.05 | 11.75 ± 0.09 | +14.94% |
| 512 | 105.30 ± 0.18 | 68.48 ± 0.44 | +53.77% | 13.41 ± 0.05 | 10.92 ± 0.24 | +22.73% |
| 1024 | 100.43 ± 0.23 | 73.38 ± 6.15 | +36.86% | 13.21 ± 0.03 | 10.61 ± 0.23 | +24.49% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
