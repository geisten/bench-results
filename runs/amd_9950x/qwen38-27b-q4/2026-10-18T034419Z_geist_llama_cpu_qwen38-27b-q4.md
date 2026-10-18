# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 105.98 ± 0.45 | 54.95 ± 0.34 | +92.85% | 4.82 ± 0.01 | 4.44 ± 0.03 | +8.62% |
| 256 | 105.95 ± 0.33 | 55.55 ± 0.17 | +90.71% | 4.82 ± 0.01 | 4.43 ± 0.02 | +8.76% |
| 512 | 105.40 ± 0.57 | 55.39 ± 0.17 | +90.28% | 4.80 ± 0.02 | 4.44 ± 0.01 | +8.12% |
| 1024 | 104.90 ± 0.29 | 55.25 ± 0.25 | +89.87% | 4.81 ± 0.01 | 4.43 ± 0.01 | +8.54% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
