# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.76 ± 1.06 | 215.20 ± 1.23 | -1.60% | 18.43 ± 0.05 | 17.66 ± 0.07 | +4.31% |
| 256 | 195.12 ± 0.24 | 210.99 ± 1.23 | -7.52% | 17.41 ± 0.06 | 16.03 ± 0.14 | +8.59% |
| 512 | 159.12 ± 0.22 | 189.79 ± 0.39 | -16.16% | 15.47 ± 0.03 | 14.34 ± 0.07 | +7.86% |
| 1024 | 106.89 ± 0.69 | 158.24 ± 0.40 | -32.45% | 12.45 ± 0.05 | 10.13 ± 0.01 | +22.93% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
