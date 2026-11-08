# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.64 ± 0.31 | 126.86 ± 1.25 | -7.27% | 13.59 ± 0.08 | 12.03 ± 0.29 | +12.94% |
| 256 | 110.35 ± 0.18 | 108.17 ± 4.92 | +2.01% | 13.52 ± 0.07 | 11.77 ± 0.10 | +14.87% |
| 512 | 105.97 ± 0.11 | 96.33 ± 6.82 | +10.02% | 13.45 ± 0.07 | 11.56 ± 0.06 | +16.38% |
| 1024 | 100.75 ± 0.17 | 94.52 ± 0.30 | +6.59% | 13.15 ± 0.10 | 11.25 ± 0.15 | +16.89% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
