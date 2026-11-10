# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.24 ± 0.77 | 212.34 ± 1.82 | -0.05% | 17.78 ± 0.09 | 17.38 ± 0.08 | +2.32% |
| 256 | 195.17 ± 0.76 | 208.31 ± 1.25 | -6.31% | 16.79 ± 0.07 | 15.82 ± 0.05 | +6.12% |
| 512 | 159.82 ± 0.36 | 187.70 ± 1.55 | -14.85% | 14.93 ± 0.08 | 14.06 ± 0.03 | +6.19% |
| 1024 | 107.93 ± 0.44 | 157.23 ± 0.30 | -31.36% | 12.04 ± 0.08 | 9.94 ± 0.03 | +21.12% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
