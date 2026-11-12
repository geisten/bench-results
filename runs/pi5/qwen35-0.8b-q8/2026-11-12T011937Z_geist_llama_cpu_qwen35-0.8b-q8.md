# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.79 ± 0.32 | 128.18 ± 3.02 | -8.11% | 13.44 ± 0.12 | 12.15 ± 0.07 | +10.64% |
| 256 | 110.63 ± 0.20 | 108.02 ± 4.68 | +2.41% | 13.41 ± 0.09 | 12.14 ± 0.14 | +10.45% |
| 512 | 105.83 ± 0.43 | 96.45 ± 0.77 | +9.73% | 13.29 ± 0.07 | 11.56 ± 0.05 | +14.95% |
| 1024 | 100.58 ± 0.25 | 94.80 ± 0.27 | +6.10% | 13.08 ± 0.12 | 11.24 ± 0.06 | +16.35% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
