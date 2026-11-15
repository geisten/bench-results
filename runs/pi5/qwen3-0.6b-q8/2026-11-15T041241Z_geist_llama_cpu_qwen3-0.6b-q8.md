# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.16 ± 0.64 | 212.88 ± 0.75 | -0.81% | 16.96 ± 0.05 | 17.30 ± 0.19 | -1.93% |
| 256 | 193.85 ± 0.74 | 208.39 ± 0.30 | -6.98% | 16.11 ± 0.07 | 15.65 ± 0.15 | +2.94% |
| 512 | 158.88 ± 0.54 | 186.30 ± 0.67 | -14.72% | 14.49 ± 0.05 | 13.95 ± 0.08 | +3.89% |
| 1024 | 107.10 ± 0.32 | 155.13 ± 1.13 | -30.96% | 11.70 ± 0.16 | 9.90 ± 0.09 | +18.27% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
