# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 958.62 ± 6.76 | 595.62 ± 3.42 | +60.94% | 52.09 ± 0.25 | 44.56 ± 0.10 | +16.89% |
| 256 | 955.14 ± 9.21 | 627.66 ± 3.19 | +52.17% | 51.66 ± 0.23 | 43.91 ± 0.05 | +17.63% |
| 512 | 950.35 ± 5.92 | 635.14 ± 2.22 | +49.63% | 51.46 ± 0.19 | 43.40 ± 0.18 | +18.58% |
| 1024 | 932.92 ± 8.25 | 618.38 ± 2.61 | +50.86% | 51.42 ± 0.18 | 43.09 ± 0.04 | +19.34% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
