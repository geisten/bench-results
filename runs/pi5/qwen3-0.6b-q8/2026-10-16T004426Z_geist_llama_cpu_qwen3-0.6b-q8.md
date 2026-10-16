# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `fda9c7a98c7b`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 77.43 ± 0.26 | 215.53 ± 0.22 | -64.08% | 18.59 ± 0.05 | 17.64 ± 0.06 | +5.39% |
| 256 | 75.24 ± 0.14 | 211.31 ± 0.39 | -64.39% | 17.49 ± 0.08 | 16.05 ± 0.09 | +8.99% |
| 512 | 69.55 ± 0.14 | 190.24 ± 0.86 | -63.44% | 15.58 ± 0.10 | 14.32 ± 0.07 | +8.77% |
| 1024 | 56.97 ± 0.09 | 158.26 ± 0.39 | -64.00% | 12.66 ± 0.09 | 10.08 ± 0.04 | +25.57% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
