# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 17.80 ± 0.12 | 27.35 ± 0.18 | -34.93% | 4.33 ± 0.03 | 3.47 ± 0.04 | +24.68% |
| 256 | 17.26 ± 0.02 | 23.58 ± 0.72 | -26.79% | 4.31 ± 0.05 | 3.43 ± 0.06 | +25.56% |
| 512 | 16.92 ± 0.05 | 22.56 ± 1.52 | -25.00% | 4.32 ± 0.03 | 3.42 ± 0.03 | +26.45% |
| 1024 | 16.38 ± 0.07 | 24.00 ± 1.52 | -31.77% | 4.24 ± 0.02 | 3.28 ± 0.02 | +29.37% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
