# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 209.43 ± 0.94 | 208.64 ± 1.55 | +0.38% | 17.40 ± 0.06 | 16.96 ± 0.17 | +2.59% |
| 256 | 192.15 ± 1.37 | 205.15 ± 0.69 | -6.33% | 16.35 ± 0.09 | 15.33 ± 0.04 | +6.63% |
| 512 | 157.74 ± 0.30 | 184.67 ± 0.74 | -14.58% | 14.60 ± 0.01 | 13.79 ± 0.06 | +5.88% |
| 1024 | 106.13 ± 0.35 | 155.04 ± 0.30 | -31.55% | 11.76 ± 0.08 | 9.72 ± 0.04 | +20.93% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
