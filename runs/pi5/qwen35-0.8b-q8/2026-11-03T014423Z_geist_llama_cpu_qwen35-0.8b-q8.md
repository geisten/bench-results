# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 116.91 ± 0.22 | 118.11 ± 6.35 | -1.02% | 13.41 ± 0.05 | 11.57 ± 0.14 | +15.89% |
| 256 | 109.44 ± 0.58 | 90.76 ± 0.99 | +20.57% | 13.39 ± 0.10 | 11.32 ± 0.15 | +18.26% |
| 512 | 105.06 ± 0.25 | 81.68 ± 0.55 | +28.63% | 13.26 ± 0.14 | 11.09 ± 0.10 | +19.54% |
| 1024 | 100.17 ± 0.10 | 80.31 ± 0.44 | +24.73% | 12.99 ± 0.07 | 10.71 ± 0.06 | +21.27% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
