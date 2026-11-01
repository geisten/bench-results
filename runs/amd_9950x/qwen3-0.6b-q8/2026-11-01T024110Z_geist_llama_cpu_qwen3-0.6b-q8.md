# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2120.44 ± 54.60 | 1625.72 ± 16.43 | +30.43% | 117.35 ± 0.48 | 106.42 ± 0.37 | +10.26% |
| 256 | 2109.78 ± 43.06 | 1670.18 ± 2.93 | +26.32% | 115.56 ± 0.48 | 107.64 ± 0.37 | +7.36% |
| 512 | 1995.70 ± 10.78 | 1673.03 ± 5.57 | +19.29% | 111.53 ± 0.40 | 102.15 ± 0.81 | +9.18% |
| 1024 | 1876.69 ± 13.39 | 1541.35 ± 6.96 | +21.76% | 105.68 ± 0.13 | 91.57 ± 0.63 | +15.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
