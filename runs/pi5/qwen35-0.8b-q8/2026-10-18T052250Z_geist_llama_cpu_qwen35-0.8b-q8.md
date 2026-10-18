# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.56 ± 0.10 | 121.49 ± 1.80 | -3.24% | 13.75 ± 0.16 | 11.45 ± 0.10 | +20.02% |
| 256 | 110.51 ± 0.40 | 96.76 ± 5.31 | +14.20% | 13.77 ± 0.09 | 11.51 ± 0.05 | +19.61% |
| 512 | 106.10 ± 0.22 | 82.31 ± 1.11 | +28.91% | 13.65 ± 0.04 | 11.30 ± 0.07 | +20.79% |
| 1024 | 101.21 ± 0.17 | 80.83 ± 0.23 | +25.22% | 13.45 ± 0.04 | 11.00 ± 0.08 | +22.31% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
