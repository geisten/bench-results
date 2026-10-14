# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `527bf29dd426`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 57.07 ± 0.11 | 130.58 ± 1.09 | -56.29% | 13.77 ± 0.04 | 12.27 ± 0.16 | +12.19% |
| 256 | 55.40 ± 0.16 | 114.61 ± 0.31 | -51.66% | 13.79 ± 0.09 | 11.95 ± 0.05 | +15.42% |
| 512 | 54.21 ± 0.16 | 110.44 ± 0.36 | -50.92% | 13.65 ± 0.06 | 11.75 ± 0.01 | +16.17% |
| 1024 | 52.88 ± 0.05 | 108.15 ± 0.42 | -51.11% | 13.33 ± 0.11 | 11.47 ± 0.04 | +16.21% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
