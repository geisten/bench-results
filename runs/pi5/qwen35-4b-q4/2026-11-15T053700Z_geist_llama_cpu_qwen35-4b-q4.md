# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 17.61 ± 0.20 | 27.46 ± 0.17 | -35.86% | 4.09 ± 0.03 | 3.49 ± 0.04 | +17.06% |
| 256 | 17.19 ± 0.11 | 21.94 ± 1.89 | -21.63% | 4.08 ± 0.02 | 3.48 ± 0.02 | +17.40% |
| 512 | 16.84 ± 0.12 | 23.34 ± 1.09 | -27.85% | 4.05 ± 0.03 | 3.41 ± 0.06 | +18.66% |
| 1024 | 16.34 ± 0.10 | 21.85 ± 0.81 | -25.21% | 3.94 ± 0.02 | 3.31 ± 0.02 | +19.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
