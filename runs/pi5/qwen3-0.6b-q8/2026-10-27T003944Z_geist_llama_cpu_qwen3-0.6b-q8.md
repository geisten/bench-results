# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `df665fe9c736`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.47 ± 0.33 | 211.21 ± 0.67 | +0.60% | 17.44 ± 0.04 | 17.54 ± 0.07 | -0.56% |
| 256 | 194.26 ± 1.01 | 206.06 ± 1.81 | -5.72% | 16.51 ± 0.07 | 15.62 ± 0.10 | +5.68% |
| 512 | 159.14 ± 0.33 | 185.36 ± 1.36 | -14.15% | 14.76 ± 0.12 | 14.13 ± 0.03 | +4.45% |
| 1024 | 106.28 ± 0.23 | 155.64 ± 0.88 | -31.72% | 11.79 ± 0.06 | 9.97 ± 0.02 | +18.30% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
