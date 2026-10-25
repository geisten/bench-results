# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.34 ± 0.72 | 215.46 ± 0.78 | -1.45% | 18.09 ± 0.11 | 17.75 ± 0.12 | +1.93% |
| 256 | 195.05 ± 0.77 | 211.00 ± 1.19 | -7.56% | 17.00 ± 0.08 | 15.97 ± 0.10 | +6.42% |
| 512 | 159.43 ± 0.29 | 189.64 ± 0.46 | -15.93% | 15.12 ± 0.14 | 14.21 ± 0.06 | +6.43% |
| 1024 | 107.96 ± 0.71 | 158.17 ± 0.74 | -31.75% | 12.18 ± 0.17 | 10.09 ± 0.04 | +20.73% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
