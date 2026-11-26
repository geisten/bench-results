# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.30 ± 0.41 | 209.35 ± 0.70 | +0.46% | 17.07 ± 0.06 | 17.04 ± 0.05 | +0.20% |
| 256 | 192.61 ± 0.56 | 205.69 ± 0.87 | -6.36% | 16.10 ± 0.08 | 15.40 ± 0.18 | +4.53% |
| 512 | 157.75 ± 0.29 | 185.09 ± 1.22 | -14.77% | 14.44 ± 0.03 | 13.82 ± 0.04 | +4.48% |
| 1024 | 106.82 ± 0.37 | 155.17 ± 0.50 | -31.16% | 11.73 ± 0.08 | 9.84 ± 0.06 | +19.28% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
