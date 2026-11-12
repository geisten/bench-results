# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.83 ± 0.67 | 211.73 ± 1.59 | +0.04% | 17.46 ± 0.09 | 17.33 ± 0.07 | +0.76% |
| 256 | 195.04 ± 0.37 | 204.87 ± 4.11 | -4.80% | 16.55 ± 0.07 | 15.66 ± 0.09 | +5.68% |
| 512 | 159.22 ± 0.22 | 186.66 ± 1.67 | -14.70% | 14.81 ± 0.09 | 14.02 ± 0.02 | +5.60% |
| 1024 | 107.14 ± 0.45 | 156.60 ± 0.67 | -31.59% | 11.93 ± 0.12 | 9.91 ± 0.04 | +20.38% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
