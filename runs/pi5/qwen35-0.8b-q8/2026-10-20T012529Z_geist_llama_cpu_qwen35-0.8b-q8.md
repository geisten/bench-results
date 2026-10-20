# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `44479afd263d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 115.42 ± 0.27 | 132.25 ± 0.92 | -12.72% | 13.82 ± 0.14 | 11.84 ± 0.06 | +16.72% |
| 256 | 108.22 ± 0.30 | 114.92 ± 0.15 | -5.83% | 13.89 ± 0.10 | 11.89 ± 0.08 | +16.82% |
| 512 | 103.77 ± 0.25 | 110.30 ± 0.49 | -5.92% | 13.79 ± 0.03 | 11.74 ± 0.08 | +17.53% |
| 1024 | 98.92 ± 0.24 | 104.98 ± 3.13 | -5.77% | 13.46 ± 0.13 | 11.45 ± 0.06 | +17.58% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
