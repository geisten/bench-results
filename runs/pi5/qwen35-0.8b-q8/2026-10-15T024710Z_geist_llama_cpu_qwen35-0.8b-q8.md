# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ebcdfb017ba6`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 57.01 ± 0.20 | 127.46 ± 1.39 | -55.28% | 13.66 ± 0.07 | 11.82 ± 0.09 | +15.60% |
| 256 | 55.34 ± 0.13 | 103.69 ± 0.49 | -46.63% | 13.57 ± 0.05 | 11.89 ± 0.09 | +14.21% |
| 512 | 54.24 ± 0.10 | 96.21 ± 0.37 | -43.62% | 13.46 ± 0.05 | 11.61 ± 0.05 | +15.96% |
| 1024 | 52.93 ± 0.08 | 95.05 ± 0.31 | -44.31% | 13.26 ± 0.06 | 11.24 ± 0.15 | +17.95% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
