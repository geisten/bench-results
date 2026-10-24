# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a9cb017fe3f5`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 118.00 ± 0.11 | 126.83 ± 2.37 | -6.96% | 13.64 ± 0.08 | 11.65 ± 0.35 | +17.08% |
| 256 | 110.45 ± 0.10 | 104.14 ± 1.53 | +6.06% | 13.61 ± 0.09 | 11.77 ± 0.11 | +15.67% |
| 512 | 105.64 ± 0.25 | 96.36 ± 0.48 | +9.63% | 13.59 ± 0.10 | 11.59 ± 0.02 | +17.19% |
| 1024 | 100.87 ± 0.15 | 95.02 ± 1.01 | +6.16% | 13.30 ± 0.13 | 11.22 ± 0.01 | +18.62% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
