# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.46 ± 1.05 | 209.06 ± 0.26 | +1.15% | 17.57 ± 0.07 | 17.06 ± 0.06 | +2.99% |
| 256 | 192.74 ± 2.14 | 202.63 ± 0.31 | -4.88% | 16.52 ± 0.08 | 15.64 ± 0.02 | +5.68% |
| 512 | 158.82 ± 0.51 | 183.50 ± 0.68 | -13.45% | 14.78 ± 0.08 | 13.92 ± 0.04 | +6.14% |
| 1024 | 106.36 ± 0.72 | 154.57 ± 0.44 | -31.19% | 11.90 ± 0.23 | 9.85 ± 0.04 | +20.76% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
