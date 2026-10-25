# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 17.46 ± 0.12 | 26.56 ± 0.93 | -34.25% | 4.31 ± 0.06 | 3.50 ± 0.03 | +23.01% |
| 256 | 17.00 ± 0.15 | 23.85 ± 0.93 | -28.70% | 4.32 ± 0.08 | 3.45 ± 0.03 | +25.04% |
| 512 | 16.67 ± 0.15 | 23.79 ± 1.42 | -29.94% | 4.27 ± 0.04 | 3.44 ± 0.03 | +24.32% |
| 1024 | 16.08 ± 0.18 | 24.00 ± 1.64 | -33.01% | 4.22 ± 0.06 | 3.25 ± 0.04 | +29.74% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
