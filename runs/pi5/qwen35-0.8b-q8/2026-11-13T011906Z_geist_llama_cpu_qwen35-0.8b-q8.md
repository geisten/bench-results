# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.11 ± 0.13 | 126.48 ± 0.55 | -7.41% | 13.49 ± 0.07 | 11.66 ± 0.24 | +15.65% |
| 256 | 109.96 ± 0.16 | 103.46 ± 0.65 | +6.29% | 13.43 ± 0.08 | 11.65 ± 0.08 | +15.24% |
| 512 | 105.09 ± 0.27 | 96.44 ± 0.31 | +8.96% | 13.35 ± 0.05 | 11.50 ± 0.03 | +16.09% |
| 1024 | 100.25 ± 0.19 | 94.60 ± 0.46 | +5.96% | 13.16 ± 0.05 | 11.19 ± 0.05 | +17.52% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
