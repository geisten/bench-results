# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 115.92 ± 0.37 | 122.63 ± 6.93 | -5.48% | 13.59 ± 0.08 | 11.34 ± 0.18 | +19.82% |
| 256 | 108.84 ± 0.15 | 97.41 ± 6.94 | +11.74% | 13.51 ± 0.08 | 11.39 ± 0.22 | +18.54% |
| 512 | 104.11 ± 0.36 | 82.12 ± 0.38 | +26.78% | 13.43 ± 0.04 | 11.00 ± 0.03 | +22.08% |
| 1024 | 99.18 ± 0.31 | 80.30 ± 0.29 | +23.51% | 13.08 ± 0.15 | 10.75 ± 0.03 | +21.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
