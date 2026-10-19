# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `20dd2b836926`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 204.10 ± 1.18 | 215.59 ± 0.24 | -5.33% | 18.74 ± 0.04 | 17.54 ± 0.05 | +6.83% |
| 256 | 188.81 ± 0.64 | 211.45 ± 0.51 | -10.71% | 17.52 ± 0.02 | 15.95 ± 0.08 | +9.83% |
| 512 | 157.25 ± 0.36 | 189.54 ± 1.57 | -17.04% | 15.47 ± 0.14 | 14.22 ± 0.07 | +8.77% |
| 1024 | 104.43 ± 0.18 | 158.90 ± 0.60 | -34.27% | 12.32 ± 0.06 | 10.04 ± 0.05 | +22.67% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
