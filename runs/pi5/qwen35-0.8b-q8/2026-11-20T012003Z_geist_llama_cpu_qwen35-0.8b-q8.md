# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.46 ± 0.31 | 114.10 ± 8.96 | +2.94% | 13.55 ± 0.07 | 11.58 ± 0.26 | +17.01% |
| 256 | 110.03 ± 0.56 | 89.84 ± 12.85 | +22.47% | 13.49 ± 0.06 | 11.83 ± 0.08 | +14.03% |
| 512 | 105.37 ± 0.49 | 74.51 ± 6.16 | +41.41% | 13.41 ± 0.03 | 10.81 ± 0.13 | +24.05% |
| 1024 | 100.56 ± 0.12 | 67.75 ± 0.38 | +48.43% | 13.17 ± 0.07 | 10.43 ± 0.06 | +26.34% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
