# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.34 ± 0.42 | 213.32 ± 0.57 | -0.46% | 17.62 ± 0.14 | 17.34 ± 0.10 | +1.63% |
| 256 | 194.04 ± 1.07 | 208.08 ± 0.89 | -6.75% | 16.70 ± 0.09 | 15.82 ± 0.07 | +5.53% |
| 512 | 159.09 ± 0.34 | 187.12 ± 1.69 | -14.98% | 14.93 ± 0.08 | 14.00 ± 0.04 | +6.62% |
| 1024 | 107.53 ± 0.72 | 157.33 ± 0.33 | -31.65% | 12.00 ± 0.10 | 9.92 ± 0.04 | +20.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
