# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 951.19 ± 6.13 | 587.66 ± 3.37 | +61.86% | 51.75 ± 0.04 | 44.49 ± 0.11 | +16.32% |
| 256 | 944.92 ± 7.65 | 625.33 ± 2.38 | +51.11% | 51.46 ± 0.11 | 43.66 ± 0.13 | +17.84% |
| 512 | 944.62 ± 2.27 | 627.43 ± 4.08 | +50.55% | 51.38 ± 0.09 | 43.31 ± 0.05 | +18.63% |
| 1024 | 927.00 ± 5.57 | 610.20 ± 4.82 | +51.92% | 51.15 ± 0.09 | 42.94 ± 0.19 | +19.12% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
