# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 209.99 ± 1.40 | 201.44 ± 4.25 | +4.24% | 17.43 ± 0.06 | 16.44 ± 0.15 | +6.01% |
| 256 | 194.19 ± 0.32 | 192.69 ± 2.22 | +0.78% | 16.44 ± 0.04 | 14.90 ± 0.14 | +10.28% |
| 512 | 158.44 ± 0.41 | 176.35 ± 1.63 | -10.16% | 14.79 ± 0.05 | 13.44 ± 0.05 | +10.00% |
| 1024 | 106.74 ± 0.54 | 150.35 ± 0.74 | -29.00% | 11.98 ± 0.10 | 9.62 ± 0.07 | +24.61% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
