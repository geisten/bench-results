# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.24 ± 0.61 | 125.42 ± 1.94 | -6.52% | 13.48 ± 0.09 | 12.14 ± 0.12 | +11.04% |
| 256 | 109.94 ± 0.72 | 101.89 ± 1.80 | +7.89% | 13.43 ± 0.07 | 11.70 ± 0.10 | +14.84% |
| 512 | 105.54 ± 0.36 | 93.34 ± 0.62 | +13.06% | 13.37 ± 0.11 | 11.53 ± 0.06 | +15.99% |
| 1024 | 100.82 ± 0.15 | 91.95 ± 0.20 | +9.64% | 13.13 ± 0.15 | 11.22 ± 0.03 | +17.07% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
