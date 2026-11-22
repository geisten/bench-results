# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 115.35 ± 0.61 | 119.18 ± 1.03 | -3.21% | 13.30 ± 0.03 | 11.18 ± 0.19 | +18.92% |
| 256 | 108.29 ± 0.30 | 90.00 ± 0.56 | +20.33% | 13.23 ± 0.08 | 11.14 ± 0.09 | +18.78% |
| 512 | 103.56 ± 0.14 | 81.02 ± 0.46 | +27.82% | 13.15 ± 0.08 | 11.00 ± 0.02 | +19.61% |
| 1024 | 98.81 ± 0.11 | 80.55 ± 0.29 | +22.68% | 12.92 ± 0.09 | 10.69 ± 0.07 | +20.85% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
