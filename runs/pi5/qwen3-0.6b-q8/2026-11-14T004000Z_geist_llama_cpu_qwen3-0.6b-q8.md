# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.54 ± 0.83 | 208.95 ± 1.49 | +0.76% | 17.89 ± 0.05 | 16.95 ± 0.06 | +5.56% |
| 256 | 194.28 ± 0.78 | 204.79 ± 3.51 | -5.13% | 16.78 ± 0.06 | 15.38 ± 0.06 | +9.12% |
| 512 | 158.53 ± 0.35 | 185.61 ± 1.33 | -14.59% | 15.03 ± 0.08 | 13.76 ± 0.07 | +9.27% |
| 1024 | 107.22 ± 0.51 | 155.21 ± 0.28 | -30.92% | 12.14 ± 0.06 | 9.73 ± 0.02 | +24.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
