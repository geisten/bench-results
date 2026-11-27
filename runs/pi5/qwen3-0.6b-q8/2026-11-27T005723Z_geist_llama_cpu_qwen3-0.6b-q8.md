# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.86 ± 0.35 | 215.84 ± 0.40 | -1.38% | 18.57 ± 0.05 | 17.73 ± 0.12 | +4.75% |
| 256 | 195.62 ± 0.59 | 209.55 ± 1.73 | -6.65% | 17.46 ± 0.08 | 15.97 ± 0.07 | +9.35% |
| 512 | 159.19 ± 0.30 | 189.52 ± 0.68 | -16.00% | 15.58 ± 0.09 | 14.28 ± 0.05 | +9.14% |
| 1024 | 107.80 ± 0.25 | 157.42 ± 0.99 | -31.53% | 12.55 ± 0.15 | 10.11 ± 0.04 | +24.22% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
