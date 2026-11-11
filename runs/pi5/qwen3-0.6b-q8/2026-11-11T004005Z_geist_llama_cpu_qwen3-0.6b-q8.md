# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.10 ± 0.38 | 208.52 ± 1.27 | +0.76% | 17.45 ± 0.09 | 17.09 ± 0.05 | +2.12% |
| 256 | 193.25 ± 0.86 | 205.14 ± 1.17 | -5.79% | 16.49 ± 0.02 | 15.33 ± 0.16 | +7.55% |
| 512 | 157.95 ± 0.67 | 184.28 ± 1.77 | -14.29% | 14.80 ± 0.03 | 13.81 ± 0.10 | +7.19% |
| 1024 | 107.13 ± 0.62 | 155.11 ± 0.46 | -30.93% | 12.03 ± 0.11 | 9.77 ± 0.04 | +23.18% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
