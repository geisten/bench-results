# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `e64ff1027649`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.79 ± 0.28 | 130.91 ± 0.67 | -10.02% | 13.83 ± 0.10 | 12.20 ± 0.18 | +13.36% |
| 256 | 110.64 ± 0.39 | 114.98 ± 0.32 | -3.77% | 13.87 ± 0.03 | 12.33 ± 0.09 | +12.48% |
| 512 | 105.92 ± 0.17 | 110.28 ± 0.51 | -3.95% | 13.76 ± 0.05 | 11.74 ± 0.07 | +17.18% |
| 1024 | 100.93 ± 0.13 | 108.01 ± 0.38 | -6.55% | 13.31 ± 0.12 | 11.36 ± 0.13 | +17.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
