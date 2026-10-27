# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `df665fe9c736`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.80 ± 0.23 | 126.32 ± 2.78 | -6.75% | 13.44 ± 0.05 | 11.68 ± 0.33 | +15.09% |
| 256 | 110.56 ± 0.22 | 102.86 ± 1.26 | +7.48% | 13.46 ± 0.10 | 11.77 ± 0.49 | +14.36% |
| 512 | 105.46 ± 0.49 | 95.62 ± 1.20 | +10.29% | 13.34 ± 0.07 | 11.59 ± 0.10 | +15.12% |
| 1024 | 100.65 ± 0.17 | 93.92 ± 0.89 | +7.16% | 13.18 ± 0.07 | 11.25 ± 0.10 | +17.11% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
