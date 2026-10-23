# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f19377734f16`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.76 ± 0.17 | 127.02 ± 4.28 | -7.29% | 13.50 ± 0.03 | 12.31 ± 0.09 | +9.72% |
| 256 | 110.62 ± 0.20 | 112.65 ± 1.99 | -1.80% | 13.41 ± 0.05 | 12.24 ± 0.16 | +9.61% |
| 512 | 105.77 ± 0.20 | 109.43 ± 0.91 | -3.34% | 13.36 ± 0.05 | 11.78 ± 0.04 | +13.41% |
| 1024 | 100.83 ± 0.16 | 101.26 ± 6.73 | -0.42% | 13.16 ± 0.04 | 11.39 ± 0.08 | +15.58% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
