# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.59 ± 0.14 | 122.29 ± 3.28 | -3.85% | 13.38 ± 0.05 | 11.78 ± 0.15 | +13.55% |
| 256 | 110.35 ± 0.18 | 100.79 ± 6.27 | +9.49% | 13.32 ± 0.10 | 12.08 ± 0.16 | +10.25% |
| 512 | 105.60 ± 0.17 | 83.29 ± 1.71 | +26.80% | 13.27 ± 0.06 | 11.43 ± 0.15 | +16.07% |
| 1024 | 100.65 ± 0.12 | 94.23 ± 6.60 | +6.82% | 12.89 ± 0.12 | 11.04 ± 0.10 | +16.76% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
