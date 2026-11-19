# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 210.94 ± 0.87 | 207.19 ± 0.79 | +1.81% | 17.43 ± 0.07 | 17.21 ± 0.09 | +1.23% |
| 256 | 194.40 ± 0.51 | 203.64 ± 3.55 | -4.54% | 16.50 ± 0.05 | 15.62 ± 0.09 | +5.64% |
| 512 | 158.23 ± 0.69 | 181.76 ± 1.18 | -12.94% | 14.79 ± 0.02 | 13.92 ± 0.06 | +6.25% |
| 1024 | 107.32 ± 0.55 | 152.68 ± 1.04 | -29.71% | 11.82 ± 0.03 | 9.76 ± 0.05 | +21.09% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
