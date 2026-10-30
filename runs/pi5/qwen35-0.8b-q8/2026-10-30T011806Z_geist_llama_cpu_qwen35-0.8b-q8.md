# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.01 ± 0.22 | 126.63 ± 3.85 | -7.60% | 13.39 ± 0.05 | 11.67 ± 0.25 | +14.77% |
| 256 | 109.51 ± 0.68 | 103.34 ± 0.76 | +5.97% | 13.37 ± 0.11 | 12.09 ± 0.13 | +10.59% |
| 512 | 105.31 ± 0.27 | 96.26 ± 0.29 | +9.41% | 13.31 ± 0.04 | 11.60 ± 0.10 | +14.77% |
| 1024 | 100.25 ± 0.17 | 94.67 ± 0.47 | +5.89% | 13.01 ± 0.10 | 11.18 ± 0.10 | +16.44% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
