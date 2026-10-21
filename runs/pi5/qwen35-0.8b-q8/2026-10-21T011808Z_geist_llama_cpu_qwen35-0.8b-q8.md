# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `24515004c598`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 115.00 ± 0.58 | 130.01 ± 0.61 | -11.54% | 13.52 ± 0.08 | 12.20 ± 0.14 | +10.82% |
| 256 | 107.79 ± 0.59 | 114.07 ± 1.09 | -5.50% | 13.48 ± 0.09 | 11.93 ± 0.21 | +12.99% |
| 512 | 103.62 ± 0.36 | 110.21 ± 0.19 | -5.97% | 13.41 ± 0.06 | 11.68 ± 0.09 | +14.89% |
| 1024 | 98.76 ± 0.22 | 107.44 ± 0.60 | -8.08% | 13.18 ± 0.04 | 11.38 ± 0.10 | +15.78% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
