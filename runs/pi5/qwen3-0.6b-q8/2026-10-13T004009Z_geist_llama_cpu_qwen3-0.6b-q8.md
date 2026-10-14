# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `db8314e2a3a3`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 77.37 ± 0.18 | 213.45 ± 2.42 | -63.75% | 17.94 ± 0.04 | 17.66 ± 0.09 | +1.62% |
| 256 | 75.13 ± 0.22 | 208.84 ± 1.57 | -64.02% | 16.92 ± 0.03 | 15.94 ± 0.16 | +6.14% |
| 512 | 69.61 ± 0.05 | 189.43 ± 0.54 | -63.25% | 14.93 ± 0.02 | 14.26 ± 0.08 | +4.68% |
| 1024 | 57.02 ± 0.07 | 157.38 ± 0.84 | -63.77% | 11.99 ± 0.03 | 10.08 ± 0.02 | +18.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
