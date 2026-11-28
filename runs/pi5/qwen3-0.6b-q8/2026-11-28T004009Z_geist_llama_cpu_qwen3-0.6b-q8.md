# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `a7a01a052466`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.77 ± 0.71 | 202.56 ± 1.36 | +4.54% | 17.73 ± 0.14 | 16.73 ± 0.08 | +5.93% |
| 256 | 194.09 ± 1.06 | 195.52 ± 1.68 | -0.73% | 16.78 ± 0.05 | 15.27 ± 0.11 | +9.88% |
| 512 | 158.41 ± 0.68 | 177.99 ± 0.48 | -11.00% | 15.06 ± 0.08 | 13.61 ± 0.04 | +10.64% |
| 1024 | 107.30 ± 0.24 | 150.35 ± 0.73 | -28.63% | 12.15 ± 0.06 | 9.63 ± 0.06 | +26.22% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
