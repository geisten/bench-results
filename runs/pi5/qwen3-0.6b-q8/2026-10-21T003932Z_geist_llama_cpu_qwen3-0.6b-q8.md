# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `24515004c598`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 203.80 ± 0.44 | 208.88 ± 3.83 | -2.43% | 17.18 ± 0.06 | 17.13 ± 0.09 | +0.26% |
| 256 | 186.52 ± 1.47 | 203.58 ± 0.76 | -8.38% | 16.20 ± 0.05 | 15.60 ± 0.12 | +3.84% |
| 512 | 153.87 ± 0.46 | 183.29 ± 1.38 | -16.05% | 14.43 ± 0.02 | 13.86 ± 0.04 | +4.12% |
| 1024 | 104.91 ± 0.97 | 154.81 ± 1.02 | -32.23% | 11.64 ± 0.04 | 9.81 ± 0.02 | +18.61% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
