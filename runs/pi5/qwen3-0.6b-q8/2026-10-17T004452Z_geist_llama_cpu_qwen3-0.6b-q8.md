# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `0b892b0f366c`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 204.91 ± 0.39 | 215.62 ± 0.25 | -4.97% | 18.61 ± 0.04 | 17.59 ± 0.09 | +5.81% |
| 256 | 189.36 ± 0.61 | 210.80 ± 0.45 | -10.17% | 17.42 ± 0.05 | 15.98 ± 0.05 | +9.01% |
| 512 | 157.93 ± 0.30 | 189.61 ± 1.07 | -16.71% | 15.50 ± 0.17 | 14.20 ± 0.06 | +9.18% |
| 1024 | 106.22 ± 0.13 | 158.66 ± 0.36 | -33.05% | 12.32 ± 0.03 | 10.06 ± 0.03 | +22.39% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
