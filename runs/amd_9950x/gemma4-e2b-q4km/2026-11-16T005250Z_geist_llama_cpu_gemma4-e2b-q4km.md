# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 944.70 ± 9.39 | 592.60 ± 3.25 | +59.42% | 51.72 ± 0.10 | 44.56 ± 0.05 | +16.07% |
| 256 | 940.97 ± 6.07 | 625.24 ± 3.62 | +50.50% | 51.54 ± 0.14 | 43.77 ± 0.11 | +17.75% |
| 512 | 933.44 ± 5.84 | 631.49 ± 2.50 | +47.82% | 51.52 ± 0.10 | 43.47 ± 0.04 | +18.51% |
| 1024 | 926.71 ± 9.26 | 613.54 ± 2.95 | +51.04% | 51.15 ± 0.16 | 43.04 ± 0.07 | +18.86% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
