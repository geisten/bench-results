# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `c212773b0268`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.91 ± 0.41 | 126.86 ± 3.92 | -7.06% | 13.57 ± 0.05 | 11.90 ± 0.31 | +14.05% |
| 256 | 110.48 ± 0.29 | 103.48 ± 7.51 | +6.76% | 13.50 ± 0.11 | 11.83 ± 0.17 | +14.10% |
| 512 | 105.89 ± 0.14 | 84.31 ± 1.96 | +25.59% | 13.31 ± 0.07 | 11.50 ± 0.16 | +15.71% |
| 1024 | 100.50 ± 0.55 | 91.13 ± 11.06 | +10.29% | 13.07 ± 0.09 | 11.23 ± 0.07 | +16.41% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
