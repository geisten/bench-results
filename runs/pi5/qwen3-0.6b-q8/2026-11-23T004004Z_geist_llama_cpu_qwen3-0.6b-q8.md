# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `b90b6b27c840`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 209.94 ± 1.55 | 208.58 ± 1.57 | +0.65% | 17.29 ± 0.07 | 17.44 ± 0.12 | -0.87% |
| 256 | 194.30 ± 0.92 | 201.93 ± 1.43 | -3.78% | 16.30 ± 0.02 | 15.86 ± 0.03 | +2.77% |
| 512 | 158.60 ± 0.30 | 183.09 ± 0.92 | -13.38% | 14.61 ± 0.06 | 14.08 ± 0.02 | +3.71% |
| 1024 | 106.54 ± 0.47 | 154.58 ± 0.83 | -31.08% | 11.81 ± 0.15 | 9.89 ± 0.05 | +19.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
