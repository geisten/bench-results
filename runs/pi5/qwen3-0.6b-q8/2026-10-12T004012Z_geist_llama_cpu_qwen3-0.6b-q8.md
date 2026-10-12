# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `4d6e2696a51b`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 77.57 ± 0.15 | 214.07 ± 0.48 | -63.76% | 17.73 ± 0.07 | 17.48 ± 0.07 | +1.43% |
| 256 | 75.44 ± 0.12 | 208.79 ± 0.28 | -63.87% | 16.76 ± 0.04 | 15.82 ± 0.02 | +5.90% |
| 512 | 70.17 ± 0.09 | 185.84 ± 2.27 | -62.24% | 14.92 ± 0.10 | 14.14 ± 0.06 | +5.52% |
| 1024 | 57.82 ± 0.15 | 157.40 ± 0.25 | -63.26% | 12.15 ± 0.17 | 9.98 ± 0.02 | +21.71% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
