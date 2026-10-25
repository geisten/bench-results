# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.81 ± 0.21 | 130.77 ± 0.54 | -9.91% | 13.71 ± 0.05 | 12.19 ± 0.19 | +12.46% |
| 256 | 110.42 ± 0.30 | 115.04 ± 0.66 | -4.01% | 13.69 ± 0.11 | 12.14 ± 0.23 | +12.71% |
| 512 | 105.96 ± 0.17 | 109.82 ± 0.83 | -3.52% | 13.58 ± 0.12 | 11.84 ± 0.06 | +14.73% |
| 1024 | 100.64 ± 0.14 | 107.94 ± 0.72 | -6.75% | 13.34 ± 0.08 | 11.46 ± 0.03 | +16.45% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
