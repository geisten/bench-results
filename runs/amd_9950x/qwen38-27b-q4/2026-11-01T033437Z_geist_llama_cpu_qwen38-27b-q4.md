# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 98.56 ± 0.94 | 55.65 ± 0.27 | +77.13% | 4.86 ± 0.01 | 4.48 ± 0.01 | +8.47% |
| 256 | 98.62 ± 1.37 | 56.27 ± 0.13 | +75.26% | 4.85 ± 0.00 | 4.47 ± 0.00 | +8.55% |
| 512 | 97.53 ± 1.67 | 55.74 ± 0.22 | +74.98% | 4.85 ± 0.01 | 4.46 ± 0.01 | +8.69% |
| 1024 | 97.16 ± 1.18 | 55.76 ± 0.16 | +74.24% | 4.83 ± 0.00 | 4.45 ± 0.00 | +8.64% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
