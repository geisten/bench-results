# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.43 ± 0.38 | 126.68 ± 2.30 | -7.30% | 13.39 ± 0.08 | 11.67 ± 0.05 | +14.75% |
| 256 | 110.45 ± 0.22 | 104.09 ± 4.39 | +6.11% | 13.32 ± 0.05 | 11.71 ± 0.04 | +13.73% |
| 512 | 105.61 ± 0.32 | 95.71 ± 0.77 | +10.34% | 13.28 ± 0.10 | 11.52 ± 0.06 | +15.30% |
| 1024 | 100.67 ± 0.30 | 94.16 ± 0.46 | +6.91% | 12.94 ± 0.12 | 11.26 ± 0.05 | +14.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
