# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 213.04 ± 0.12 | 215.16 ± 1.06 | -0.99% | 17.46 ± 0.12 | 17.89 ± 0.07 | -2.43% |
| 256 | 195.53 ± 0.22 | 210.05 ± 1.41 | -6.91% | 16.46 ± 0.09 | 15.93 ± 0.08 | +3.37% |
| 512 | 159.77 ± 0.18 | 189.53 ± 1.78 | -15.70% | 14.75 ± 0.07 | 14.27 ± 0.04 | +3.38% |
| 1024 | 106.07 ± 0.77 | 158.62 ± 0.39 | -33.13% | 11.94 ± 0.13 | 10.07 ± 0.04 | +18.48% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
