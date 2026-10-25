# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 97.30 ± 1.05 | 54.22 ± 0.15 | +79.45% | 4.82 ± 0.01 | 4.37 ± 0.03 | +10.49% |
| 256 | 94.75 ± 1.16 | 54.82 ± 0.10 | +72.85% | 4.81 ± 0.02 | 4.39 ± 0.06 | +9.63% |
| 512 | 94.53 ± 0.62 | 53.54 ± 0.53 | +76.57% | 4.82 ± 0.01 | 4.37 ± 0.04 | +10.33% |
| 1024 | 94.88 ± 1.41 | 53.81 ± 0.72 | +76.34% | 4.80 ± 0.02 | 4.35 ± 0.01 | +10.11% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
