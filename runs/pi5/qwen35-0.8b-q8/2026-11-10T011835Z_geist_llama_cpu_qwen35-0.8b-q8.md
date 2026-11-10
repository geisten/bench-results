# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.88 ± 0.15 | 127.05 ± 4.21 | -7.22% | 13.54 ± 0.04 | 11.79 ± 0.05 | +14.83% |
| 256 | 110.18 ± 0.40 | 103.39 ± 1.37 | +6.57% | 13.50 ± 0.03 | 11.85 ± 0.15 | +13.92% |
| 512 | 105.82 ± 0.11 | 96.48 ± 0.59 | +9.68% | 13.43 ± 0.02 | 11.57 ± 0.04 | +16.08% |
| 1024 | 100.56 ± 0.24 | 94.65 ± 0.18 | +6.25% | 13.20 ± 0.04 | 11.37 ± 0.03 | +16.15% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
