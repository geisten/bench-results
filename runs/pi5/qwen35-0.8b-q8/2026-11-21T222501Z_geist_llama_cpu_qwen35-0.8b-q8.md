# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.80 ± 0.17 | 124.63 ± 3.37 | -5.48% | 13.86 ± 0.06 | 11.72 ± 0.22 | +18.18% |
| 256 | 110.19 ± 0.26 | 90.79 ± 6.38 | +21.37% | 13.64 ± 0.03 | 11.55 ± 0.06 | +18.02% |
| 512 | 105.83 ± 0.17 | 83.47 ± 7.18 | +26.78% | 13.60 ± 0.06 | 11.40 ± 0.07 | +19.34% |
| 1024 | 100.75 ± 0.20 | 80.41 ± 6.88 | +25.29% | 13.33 ± 0.08 | 11.07 ± 0.04 | +20.49% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
