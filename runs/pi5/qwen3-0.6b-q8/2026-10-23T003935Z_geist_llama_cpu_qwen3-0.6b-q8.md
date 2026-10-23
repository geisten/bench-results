# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `cdc4ba43c58a`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.07 ± 0.27 | 210.25 ± 2.88 | +0.86% | 17.81 ± 0.11 | 17.33 ± 0.08 | +2.80% |
| 256 | 194.75 ± 0.55 | 208.10 ± 0.57 | -6.41% | 16.77 ± 0.10 | 15.76 ± 0.09 | +6.39% |
| 512 | 158.75 ± 0.12 | 187.21 ± 1.15 | -15.20% | 14.89 ± 0.11 | 14.02 ± 0.07 | +6.20% |
| 1024 | 106.64 ± 0.28 | 156.15 ± 0.73 | -31.71% | 11.92 ± 0.07 | 9.88 ± 0.06 | +20.68% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
