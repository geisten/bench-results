# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.72 ± 0.20 | 122.53 ± 6.01 | -3.93% | 13.65 ± 0.04 | 11.85 ± 0.25 | +15.18% |
| 256 | 110.40 ± 0.25 | 95.66 ± 12.75 | +15.41% | 13.59 ± 0.09 | 11.50 ± 0.12 | +18.11% |
| 512 | 105.61 ± 0.16 | 83.12 ± 10.74 | +27.05% | 13.58 ± 0.10 | 11.46 ± 0.14 | +18.48% |
| 1024 | 100.61 ± 0.13 | 80.66 ± 0.43 | +24.73% | 13.39 ± 0.08 | 11.00 ± 0.03 | +21.73% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
