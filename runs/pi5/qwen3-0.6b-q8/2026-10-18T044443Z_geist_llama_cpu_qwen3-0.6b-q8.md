# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 205.07 ± 0.50 | 214.43 ± 2.21 | -4.37% | 18.21 ± 0.06 | 17.72 ± 0.04 | +2.74% |
| 256 | 190.46 ± 0.24 | 210.29 ± 1.26 | -9.43% | 17.13 ± 0.05 | 15.99 ± 0.04 | +7.13% |
| 512 | 159.89 ± 0.14 | 190.26 ± 0.37 | -15.97% | 15.18 ± 0.03 | 14.19 ± 0.06 | +7.03% |
| 1024 | 106.17 ± 0.26 | 158.31 ± 0.28 | -32.94% | 12.18 ± 0.02 | 10.08 ± 0.02 | +20.88% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
