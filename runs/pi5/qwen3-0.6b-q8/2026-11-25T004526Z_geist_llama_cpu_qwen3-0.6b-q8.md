# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 213.05 ± 0.20 | 215.10 ± 0.32 | -0.95% | 18.39 ± 0.17 | 17.68 ± 0.12 | +4.03% |
| 256 | 195.30 ± 0.67 | 211.44 ± 0.65 | -7.63% | 17.37 ± 0.05 | 16.02 ± 0.12 | +8.48% |
| 512 | 159.25 ± 0.17 | 188.81 ± 0.70 | -15.65% | 15.50 ± 0.06 | 14.23 ± 0.02 | +8.91% |
| 1024 | 108.07 ± 0.16 | 158.80 ± 0.53 | -31.95% | 12.47 ± 0.03 | 10.07 ± 0.05 | +23.80% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
