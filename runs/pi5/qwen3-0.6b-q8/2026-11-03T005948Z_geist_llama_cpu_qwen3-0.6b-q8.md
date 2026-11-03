# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.10 ± 0.36 | 213.25 ± 1.65 | -1.01% | 17.73 ± 0.04 | 17.49 ± 0.05 | +1.39% |
| 256 | 193.77 ± 0.83 | 206.32 ± 2.67 | -6.08% | 16.71 ± 0.04 | 15.74 ± 0.11 | +6.15% |
| 512 | 158.86 ± 0.24 | 187.58 ± 0.71 | -15.31% | 14.99 ± 0.04 | 14.15 ± 0.03 | +5.91% |
| 1024 | 107.24 ± 0.78 | 157.28 ± 0.68 | -31.82% | 12.21 ± 0.07 | 9.95 ± 0.05 | +22.64% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
