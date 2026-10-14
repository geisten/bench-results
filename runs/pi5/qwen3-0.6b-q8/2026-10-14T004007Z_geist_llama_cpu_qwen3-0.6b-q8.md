# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `527bf29dd426`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 77.52 ± 0.08 | 212.75 ± 1.48 | -63.56% | 17.72 ± 0.05 | 17.52 ± 0.10 | +1.16% |
| 256 | 75.12 ± 0.08 | 209.20 ± 0.47 | -64.09% | 16.70 ± 0.02 | 15.84 ± 0.05 | +5.41% |
| 512 | 69.53 ± 0.10 | 187.78 ± 1.11 | -62.97% | 14.83 ± 0.03 | 14.13 ± 0.04 | +4.98% |
| 1024 | 57.11 ± 0.11 | 157.02 ± 0.26 | -63.63% | 12.04 ± 0.16 | 10.00 ± 0.03 | +20.41% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
