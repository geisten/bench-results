# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `a9cb017fe3f5`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.77 ± 0.72 | 211.95 ± 1.11 | +0.39% | 18.00 ± 0.05 | 17.40 ± 0.08 | +3.49% |
| 256 | 195.52 ± 0.32 | 207.96 ± 1.21 | -5.98% | 16.93 ± 0.07 | 15.79 ± 0.08 | +7.21% |
| 512 | 159.59 ± 0.20 | 187.78 ± 0.74 | -15.01% | 15.04 ± 0.01 | 14.09 ± 0.07 | +6.72% |
| 1024 | 106.31 ± 0.52 | 156.34 ± 0.66 | -32.00% | 12.11 ± 0.07 | 9.95 ± 0.01 | +21.65% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
