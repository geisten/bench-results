# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 98.87 ± 1.19 | 55.61 ± 0.28 | +77.79% | 4.86 ± 0.00 | 4.50 ± 0.00 | +7.94% |
| 256 | 99.63 ± 0.60 | 55.99 ± 0.13 | +77.93% | 4.86 ± 0.00 | 4.49 ± 0.01 | +8.15% |
| 512 | 99.12 ± 1.25 | 55.68 ± 0.21 | +78.02% | 4.85 ± 0.01 | 4.49 ± 0.01 | +8.16% |
| 1024 | 97.01 ± 0.86 | 55.51 ± 0.20 | +74.76% | 4.85 ± 0.00 | 4.47 ± 0.01 | +8.53% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
