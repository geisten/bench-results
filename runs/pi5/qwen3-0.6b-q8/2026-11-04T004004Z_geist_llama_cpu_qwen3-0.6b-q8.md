# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `pi5`: 4-thread prefill, 3-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Cortex-A76 (unavailable physical cores), Linux 6.18.33+rpt-rpi-2712.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 212.49 ± 0.38 | 213.93 ± 1.67 | -0.67% | 17.49 ± 0.08 | 17.62 ± 0.09 | -0.71% |
| 256 | 195.58 ± 0.59 | 208.55 ± 1.74 | -6.22% | 16.51 ± 0.04 | 15.84 ± 0.06 | +4.18% |
| 512 | 159.91 ± 0.08 | 189.02 ± 1.67 | -15.40% | 14.72 ± 0.03 | 14.23 ± 0.03 | +3.41% |
| 1024 | 107.67 ± 0.16 | 158.14 ± 0.50 | -31.92% | 11.91 ± 0.04 | 10.02 ± 0.03 | +18.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
