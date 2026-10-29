# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `c212773b0268`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.11 ± 0.58 | 204.97 ± 3.83 | +3.00% | 17.84 ± 0.06 | 16.91 ± 0.11 | +5.47% |
| 256 | 194.47 ± 0.21 | 201.71 ± 1.03 | -3.59% | 16.74 ± 0.06 | 15.34 ± 0.09 | +9.13% |
| 512 | 158.52 ± 0.43 | 183.50 ± 0.86 | -13.61% | 14.96 ± 0.08 | 13.70 ± 0.05 | +9.26% |
| 1024 | 107.19 ± 0.41 | 153.83 ± 0.41 | -30.32% | 12.09 ± 0.06 | 9.71 ± 0.03 | +24.50% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
