# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `2b5263f87833`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 115.03 ± 0.43 | 127.19 ± 2.17 | -9.56% | 13.73 ± 0.08 | 12.33 ± 0.07 | +11.38% |
| 256 | 108.19 ± 0.18 | 102.68 ± 6.97 | +5.36% | 13.69 ± 0.13 | 12.07 ± 0.23 | +13.46% |
| 512 | 103.99 ± 0.27 | 95.41 ± 1.14 | +8.99% | 13.76 ± 0.03 | 11.69 ± 0.08 | +17.70% |
| 1024 | 99.20 ± 0.08 | 93.67 ± 0.97 | +5.90% | 13.43 ± 0.14 | 11.35 ± 0.02 | +18.30% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
