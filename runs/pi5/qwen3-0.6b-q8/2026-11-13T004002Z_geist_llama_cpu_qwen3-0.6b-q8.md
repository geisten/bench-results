# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.51 ± 0.80 | 209.62 ± 5.39 | +0.90% | 17.41 ± 0.05 | 17.61 ± 0.04 | -1.15% |
| 256 | 192.98 ± 1.50 | 205.96 ± 2.49 | -6.30% | 16.45 ± 0.03 | 15.89 ± 0.04 | +3.52% |
| 512 | 159.08 ± 0.51 | 185.53 ± 1.30 | -14.26% | 14.75 ± 0.10 | 14.09 ± 0.05 | +4.70% |
| 1024 | 107.45 ± 0.36 | 156.45 ± 0.68 | -31.32% | 11.99 ± 0.18 | 10.01 ± 0.08 | +19.76% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
