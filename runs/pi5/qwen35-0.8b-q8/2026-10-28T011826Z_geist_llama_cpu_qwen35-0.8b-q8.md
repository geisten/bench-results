# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `13921becb240`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 116.91 ± 0.52 | 126.32 ± 2.34 | -7.45% | 13.35 ± 0.05 | 11.97 ± 0.14 | +11.53% |
| 256 | 109.68 ± 0.36 | 101.38 ± 0.86 | +8.19% | 13.27 ± 0.08 | 11.92 ± 0.10 | +11.31% |
| 512 | 104.87 ± 0.28 | 94.82 ± 0.46 | +10.59% | 13.19 ± 0.04 | 11.36 ± 0.05 | +16.07% |
| 1024 | 100.15 ± 0.24 | 92.94 ± 0.46 | +7.76% | 12.96 ± 0.06 | 11.09 ± 0.03 | +16.90% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
