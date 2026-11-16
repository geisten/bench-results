# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.58 ± 0.34 | 130.82 ± 0.55 | -10.12% | 13.62 ± 0.05 | 11.90 ± 0.21 | +14.47% |
| 256 | 110.59 ± 0.23 | 113.14 ± 1.75 | -2.25% | 13.58 ± 0.05 | 11.88 ± 0.29 | +14.26% |
| 512 | 105.63 ± 0.27 | 96.84 ± 2.03 | +9.08% | 13.46 ± 0.06 | 11.74 ± 0.15 | +14.66% |
| 1024 | 100.58 ± 0.33 | 107.85 ± 0.56 | -6.74% | 13.12 ± 0.14 | 11.32 ± 0.10 | +15.90% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
