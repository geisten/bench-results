# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `44479afd263d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 205.41 ± 0.90 | 215.90 ± 0.39 | -4.86% | 18.60 ± 0.09 | 17.65 ± 0.19 | +5.35% |
| 256 | 188.86 ± 0.56 | 211.38 ± 0.55 | -10.65% | 17.46 ± 0.07 | 15.96 ± 0.09 | +9.41% |
| 512 | 155.46 ± 0.14 | 189.83 ± 0.75 | -18.11% | 15.57 ± 0.01 | 14.22 ± 0.07 | +9.45% |
| 1024 | 105.37 ± 0.20 | 158.43 ± 0.76 | -33.49% | 12.46 ± 0.05 | 10.11 ± 0.05 | +23.33% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
