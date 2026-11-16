# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 211.21 ± 0.81 | 212.83 ± 2.14 | -0.76% | 17.44 ± 0.02 | 17.33 ± 0.11 | +0.62% |
| 256 | 194.15 ± 0.89 | 207.63 ± 1.10 | -6.49% | 16.46 ± 0.04 | 15.85 ± 0.10 | +3.89% |
| 512 | 158.43 ± 0.21 | 187.51 ± 0.89 | -15.51% | 14.64 ± 0.05 | 14.02 ± 0.04 | +4.44% |
| 1024 | 106.91 ± 0.62 | 157.38 ± 1.14 | -32.07% | 11.76 ± 0.07 | 9.97 ± 0.08 | +17.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
