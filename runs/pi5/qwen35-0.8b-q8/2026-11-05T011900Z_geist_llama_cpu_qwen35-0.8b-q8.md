# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `406a3c0519ec`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.69 ± 0.29 | 127.62 ± 1.61 | -7.78% | 13.74 ± 0.04 | 11.86 ± 0.21 | +15.85% |
| 256 | 109.85 ± 0.64 | 108.96 ± 6.19 | +0.82% | 13.67 ± 0.07 | 12.10 ± 0.14 | +12.94% |
| 512 | 105.27 ± 0.41 | 98.39 ± 2.43 | +7.00% | 13.48 ± 0.15 | 11.57 ± 0.05 | +16.51% |
| 1024 | 100.71 ± 0.24 | 94.60 ± 0.41 | +6.46% | 13.27 ± 0.16 | 11.17 ± 0.11 | +18.87% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
