# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `4d6e2696a51b`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 67.00 ± 0.40 | 125.58 ± 3.21 | -46.65% | 13.87 ± 0.05 | 11.96 ± 0.27 | +15.97% |
| 256 | 66.78 ± 0.11 | 103.65 ± 3.64 | -35.57% | 13.77 ± 0.06 | 11.97 ± 0.24 | +15.05% |
| 512 | 66.04 ± 0.07 | 96.12 ± 1.06 | -31.29% | 13.70 ± 0.04 | 11.48 ± 0.06 | +19.38% |
| 1024 | 64.48 ± 0.20 | 95.03 ± 0.25 | -32.14% | 13.51 ± 0.02 | 11.22 ± 0.06 | +20.36% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
