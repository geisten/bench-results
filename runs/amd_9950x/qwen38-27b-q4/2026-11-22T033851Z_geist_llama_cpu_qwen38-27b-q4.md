# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.8-27b-q4_0.gguf` (`ede16c7b36e578ca87a8c70e011e4b4633a32c831c0ce76d0f474582384e671d`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 95.22 ± 1.37 | 54.73 ± 0.29 | +74.00% | 4.84 ± 0.00 | 4.47 ± 0.00 | +8.27% |
| 256 | 95.66 ± 0.56 | 55.23 ± 0.18 | +73.20% | 4.83 ± 0.01 | 4.47 ± 0.01 | +8.11% |
| 512 | 93.96 ± 2.11 | 54.32 ± 0.68 | +72.97% | 4.82 ± 0.01 | 4.46 ± 0.01 | +8.01% |
| 1024 | 93.33 ± 1.49 | 54.18 ± 1.02 | +72.27% | 4.82 ± 0.01 | 4.44 ± 0.00 | +8.62% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
