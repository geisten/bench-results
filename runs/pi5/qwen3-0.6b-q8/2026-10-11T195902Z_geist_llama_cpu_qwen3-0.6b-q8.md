# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `6629d2335c4d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 77.87 ± 0.07 | 214.75 ± 0.25 | -63.74% | 18.09 ± 0.16 | 17.78 ± 0.17 | +1.73% |
| 256 | 75.49 ± 0.11 | 209.25 ± 0.92 | -63.92% | 16.87 ± 0.12 | 15.79 ± 0.04 | +6.81% |
| 512 | 69.99 ± 0.23 | 187.61 ± 0.84 | -62.69% | 15.15 ± 0.16 | 14.37 ± 0.08 | +5.40% |
| 1024 | 57.77 ± 0.34 | 157.37 ± 0.36 | -63.29% | 12.38 ± 0.15 | 10.07 ± 0.02 | +22.93% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
