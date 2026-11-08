# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.91 ± 0.35 | 210.47 ± 2.03 | +0.21% | 17.68 ± 0.10 | 16.89 ± 0.14 | +4.73% |
| 256 | 194.67 ± 0.50 | 205.27 ± 2.48 | -5.16% | 16.69 ± 0.07 | 15.37 ± 0.10 | +8.58% |
| 512 | 158.95 ± 0.38 | 186.12 ± 0.79 | -14.60% | 14.87 ± 0.08 | 13.79 ± 0.10 | +7.81% |
| 1024 | 107.09 ± 0.31 | 156.07 ± 0.53 | -31.38% | 12.02 ± 0.04 | 9.76 ± 0.06 | +23.12% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
