# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `406a3c0519ec`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.70 ± 0.51 | 212.28 ± 1.15 | +0.20% | 17.84 ± 0.06 | 17.29 ± 0.07 | +3.16% |
| 256 | 195.84 ± 0.27 | 207.74 ± 0.97 | -5.73% | 16.83 ± 0.07 | 15.73 ± 0.09 | +7.00% |
| 512 | 159.59 ± 0.32 | 187.09 ± 1.35 | -14.70% | 15.10 ± 0.03 | 14.02 ± 0.06 | +7.69% |
| 1024 | 107.12 ± 0.21 | 156.93 ± 0.25 | -31.74% | 12.19 ± 0.02 | 9.96 ± 0.03 | +22.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
