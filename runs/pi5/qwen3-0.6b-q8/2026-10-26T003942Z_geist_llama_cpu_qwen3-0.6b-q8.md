# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `eedaae6cae7b`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.66 ± 0.56 | 212.43 ± 1.18 | -0.36% | 17.61 ± 0.04 | 17.33 ± 0.10 | +1.59% |
| 256 | 194.75 ± 0.44 | 208.13 ± 1.24 | -6.43% | 16.59 ± 0.06 | 15.75 ± 0.09 | +5.35% |
| 512 | 158.85 ± 0.35 | 188.16 ± 0.35 | -15.58% | 14.88 ± 0.07 | 14.11 ± 0.06 | +5.47% |
| 1024 | 106.65 ± 0.26 | 156.74 ± 0.46 | -31.96% | 12.10 ± 0.06 | 9.91 ± 0.03 | +22.07% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
