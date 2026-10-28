# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `13921becb240`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.91 ± 0.51 | 210.26 ± 0.63 | +0.31% | 16.89 ± 0.05 | 16.98 ± 0.06 | -0.57% |
| 256 | 193.26 ± 1.41 | 205.34 ± 0.81 | -5.88% | 15.97 ± 0.03 | 15.36 ± 0.17 | +4.03% |
| 512 | 157.78 ± 0.55 | 185.08 ± 1.16 | -14.75% | 14.25 ± 0.07 | 13.79 ± 0.07 | +3.32% |
| 1024 | 106.94 ± 0.35 | 155.58 ± 0.19 | -31.27% | 11.56 ± 0.15 | 9.79 ± 0.02 | +18.03% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
