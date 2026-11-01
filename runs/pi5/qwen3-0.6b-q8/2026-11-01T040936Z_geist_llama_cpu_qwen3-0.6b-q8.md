# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.00 ± 0.22 | 208.54 ± 1.17 | +0.70% | 16.91 ± 0.08 | 16.96 ± 0.07 | -0.27% |
| 256 | 193.78 ± 0.34 | 203.67 ± 2.05 | -4.86% | 15.98 ± 0.05 | 15.35 ± 0.09 | +4.11% |
| 512 | 157.88 ± 0.52 | 184.80 ± 1.09 | -14.57% | 14.30 ± 0.08 | 13.69 ± 0.03 | +4.44% |
| 1024 | 107.69 ± 0.32 | 154.45 ± 0.77 | -30.28% | 11.49 ± 0.18 | 9.75 ± 0.04 | +17.86% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
