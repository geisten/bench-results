# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `13a57a14f48f`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.77 ± 0.78 | 210.91 ± 3.28 | +0.41% | 17.76 ± 0.09 | 17.27 ± 0.11 | +2.85% |
| 256 | 194.65 ± 0.41 | 204.90 ± 4.11 | -5.00% | 16.84 ± 0.08 | 15.66 ± 0.11 | +7.55% |
| 512 | 159.09 ± 0.10 | 188.08 ± 0.68 | -15.42% | 15.01 ± 0.06 | 14.02 ± 0.05 | +7.02% |
| 1024 | 106.69 ± 0.10 | 156.62 ± 0.37 | -31.88% | 11.99 ± 0.06 | 9.93 ± 0.03 | +20.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
