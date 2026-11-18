# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 116.95 ± 0.91 | 131.50 ± 0.66 | -11.07% | 13.53 ± 0.08 | 12.13 ± 0.27 | +11.53% |
| 256 | 110.01 ± 0.65 | 108.21 ± 4.95 | +1.67% | 13.50 ± 0.05 | 11.83 ± 0.12 | +14.11% |
| 512 | 105.68 ± 0.15 | 103.39 ± 7.01 | +2.21% | 13.36 ± 0.06 | 11.62 ± 0.22 | +14.93% |
| 1024 | 100.55 ± 0.19 | 99.15 ± 6.80 | +1.42% | 13.08 ± 0.13 | 11.22 ± 0.03 | +16.55% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
