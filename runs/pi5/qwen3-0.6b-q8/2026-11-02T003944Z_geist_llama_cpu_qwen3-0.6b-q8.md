# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `e64ff1027649`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.62 ± 0.57 | 215.78 ± 0.42 | -1.47% | 18.45 ± 0.07 | 17.63 ± 0.03 | +4.66% |
| 256 | 194.89 ± 0.79 | 211.08 ± 0.37 | -7.67% | 17.36 ± 0.04 | 16.00 ± 0.04 | +8.48% |
| 512 | 159.27 ± 0.43 | 190.03 ± 0.55 | -16.19% | 15.50 ± 0.05 | 14.23 ± 0.05 | +8.96% |
| 1024 | 107.99 ± 0.12 | 158.71 ± 0.53 | -31.96% | 12.43 ± 0.15 | 10.10 ± 0.04 | +23.03% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
