# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a1751c84f0d4`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 117.45 ± 0.40 | 118.61 ± 2.32 | -0.97% | 13.49 ± 0.04 | 12.01 ± 0.24 | +12.38% |
| 256 | 110.46 ± 0.23 | 95.21 ± 4.52 | +16.01% | 13.47 ± 0.04 | 11.56 ± 0.23 | +16.49% |
| 512 | 105.45 ± 0.24 | 82.80 ± 4.69 | +27.37% | 13.37 ± 0.03 | 11.32 ± 0.07 | +18.09% |
| 1024 | 100.58 ± 0.07 | 80.90 ± 0.73 | +24.33% | 13.16 ± 0.03 | 10.91 ± 0.07 | +20.60% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
