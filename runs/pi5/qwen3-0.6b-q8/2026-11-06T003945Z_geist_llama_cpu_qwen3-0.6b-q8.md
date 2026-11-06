# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.04 ± 1.97 | 212.68 ± 1.00 | -1.24% | 17.60 ± 0.06 | 17.48 ± 0.10 | +0.68% |
| 256 | 194.64 ± 0.55 | 207.75 ± 0.58 | -6.31% | 16.62 ± 0.03 | 15.73 ± 0.07 | +5.70% |
| 512 | 158.88 ± 0.54 | 187.68 ± 0.79 | -15.35% | 14.77 ± 0.07 | 14.01 ± 0.05 | +5.46% |
| 1024 | 106.17 ± 0.74 | 156.94 ± 0.77 | -32.35% | 11.82 ± 0.09 | 9.94 ± 0.01 | +18.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
