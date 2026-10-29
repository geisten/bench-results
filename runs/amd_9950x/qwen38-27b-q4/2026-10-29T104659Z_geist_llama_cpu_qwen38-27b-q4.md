# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `1515c60147c9`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 73.55 ± 0.52 | 47.67 ± 0.12 | +54.28% | 4.80 ± 0.00 | 4.42 ± 0.00 | +8.55% |
| 256 | 73.22 ± 0.49 | 48.33 ± 0.05 | +51.51% | 4.81 ± 0.01 | 4.42 ± 0.01 | +8.82% |
| 512 | 73.12 ± 0.46 | 50.93 ± 0.69 | +43.57% | 4.80 ± 0.01 | 4.41 ± 0.01 | +8.83% |
| 1024 | 72.98 ± 0.62 | 50.31 ± 0.80 | +45.06% | 4.79 ± 0.01 | 4.40 ± 0.00 | +8.88% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
