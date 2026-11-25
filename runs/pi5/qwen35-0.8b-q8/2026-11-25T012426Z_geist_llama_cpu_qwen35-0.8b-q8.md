# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.79 ± 0.17 | 123.83 ± 2.43 | -4.88% | 13.81 ± 0.08 | 12.01 ± 0.07 | +14.95% |
| 256 | 110.50 ± 0.23 | 101.12 ± 0.95 | +9.28% | 13.72 ± 0.06 | 11.80 ± 0.07 | +16.30% |
| 512 | 105.54 ± 0.29 | 94.81 ± 1.45 | +11.32% | 13.63 ± 0.11 | 11.50 ± 0.09 | +18.50% |
| 1024 | 100.69 ± 0.10 | 92.27 ± 1.28 | +9.13% | 13.42 ± 0.14 | 11.07 ± 0.18 | +21.23% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
