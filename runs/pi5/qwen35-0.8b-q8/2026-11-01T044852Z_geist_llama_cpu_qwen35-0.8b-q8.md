# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.09 ± 0.52 | 126.69 ± 3.70 | -7.58% | 13.49 ± 0.11 | 11.66 ± 0.46 | +15.63% |
| 256 | 110.16 ± 0.36 | 102.58 ± 7.16 | +7.39% | 13.40 ± 0.03 | 11.61 ± 0.15 | +15.39% |
| 512 | 105.74 ± 0.17 | 94.98 ± 0.47 | +11.32% | 13.31 ± 0.03 | 11.42 ± 0.22 | +16.58% |
| 1024 | 100.47 ± 0.32 | 94.17 ± 0.93 | +6.69% | 12.98 ± 0.09 | 11.03 ± 0.15 | +17.60% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
