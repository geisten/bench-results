# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b892b0f366c`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 118.38 ± 0.21 | 125.81 ± 2.04 | -5.91% | 13.85 ± 0.02 | 11.81 ± 0.09 | +17.24% |
| 256 | 111.05 ± 0.38 | 85.27 ± 7.64 | +30.24% | 13.85 ± 0.08 | 11.87 ± 0.18 | +16.68% |
| 512 | 106.78 ± 0.14 | 78.51 ± 6.72 | +36.01% | 13.69 ± 0.04 | 11.52 ± 0.07 | +18.84% |
| 1024 | 101.80 ± 0.07 | 73.75 ± 5.68 | +38.03% | 13.54 ± 0.08 | 11.10 ± 0.15 | +21.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
