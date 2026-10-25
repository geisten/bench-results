# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1463.84 ± 23.59 | 1138.17 ± 9.11 | +28.61% | 114.50 ± 0.47 | 103.12 ± 0.29 | +11.04% |
| 256 | 1473.17 ± 15.82 | 1172.75 ± 2.11 | +25.62% | 112.64 ± 0.68 | 104.74 ± 0.67 | +7.54% |
| 512 | 1424.84 ± 16.11 | 1157.32 ± 1.94 | +23.12% | 108.26 ± 0.44 | 99.56 ± 1.06 | +8.74% |
| 1024 | 1349.78 ± 8.47 | 1090.31 ± 2.53 | +23.80% | 102.57 ± 0.15 | 89.21 ± 0.13 | +14.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
