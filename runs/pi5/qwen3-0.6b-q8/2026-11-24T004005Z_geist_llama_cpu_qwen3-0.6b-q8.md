# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.26 ± 0.88 | 207.24 ± 1.89 | +1.45% | 17.81 ± 0.09 | 17.06 ± 0.08 | +4.37% |
| 256 | 193.86 ± 0.84 | 202.17 ± 0.75 | -4.11% | 16.83 ± 0.09 | 15.53 ± 0.05 | +8.39% |
| 512 | 158.55 ± 0.29 | 183.23 ± 2.73 | -13.47% | 14.96 ± 0.05 | 13.83 ± 0.03 | +8.13% |
| 1024 | 107.54 ± 0.43 | 153.18 ± 0.71 | -29.79% | 12.00 ± 0.10 | 9.77 ± 0.06 | +22.80% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
