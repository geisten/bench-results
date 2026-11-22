# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.11 ± 0.53 | 209.59 ± 1.20 | +0.72% | 17.95 ± 0.07 | 16.94 ± 0.15 | +5.94% |
| 256 | 193.97 ± 0.52 | 202.30 ± 0.58 | -4.12% | 16.98 ± 0.04 | 15.44 ± 0.11 | +9.94% |
| 512 | 158.64 ± 0.14 | 182.26 ± 2.14 | -12.96% | 15.17 ± 0.05 | 13.77 ± 0.09 | +10.16% |
| 1024 | 106.89 ± 0.18 | 152.90 ± 1.12 | -30.09% | 12.16 ± 0.12 | 9.73 ± 0.08 | +24.93% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
