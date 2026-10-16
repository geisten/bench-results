# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `fda9c7a98c7b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 778.63 ± 104.18 | 564.79 ± 29.66 | +37.86% | 51.54 ± 0.38 | 44.22 ± 0.14 | +16.56% |
| 256 | 820.83 ± 123.71 | 592.24 ± 30.61 | +38.60% | 51.25 ± 0.42 | 43.43 ± 0.25 | +18.00% |
| 512 | 810.49 ± 119.83 | 590.06 ± 33.31 | +37.36% | 50.97 ± 0.26 | 43.05 ± 0.19 | +18.38% |
| 1024 | 804.33 ± 120.71 | 577.66 ± 36.14 | +39.24% | 50.87 ± 0.41 | 42.61 ± 0.24 | +19.38% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
