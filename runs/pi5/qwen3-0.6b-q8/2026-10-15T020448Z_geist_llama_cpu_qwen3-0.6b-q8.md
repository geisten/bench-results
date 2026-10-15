# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `ebcdfb017ba6`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 77.60 ± 0.15 | 209.29 ± 0.79 | -62.92% | 18.63 ± 0.04 | 17.23 ± 0.17 | +8.08% |
| 256 | 75.27 ± 0.11 | 202.89 ± 0.57 | -62.90% | 17.39 ± 0.05 | 15.60 ± 0.10 | +11.48% |
| 512 | 69.65 ± 0.07 | 182.76 ± 1.50 | -61.89% | 15.45 ± 0.08 | 13.99 ± 0.11 | +10.46% |
| 1024 | 57.32 ± 0.04 | 154.80 ± 0.89 | -62.97% | 12.41 ± 0.09 | 9.90 ± 0.03 | +25.34% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
