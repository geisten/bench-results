# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 941.41 ± 8.14 | 593.70 ± 3.50 | +58.57% | 51.94 ± 0.21 | 44.89 ± 0.15 | +15.69% |
| 256 | 953.78 ± 12.58 | 625.95 ± 2.19 | +52.37% | 51.63 ± 0.11 | 44.23 ± 0.07 | +16.72% |
| 512 | 940.37 ± 5.69 | 634.45 ± 2.26 | +48.22% | 51.46 ± 0.15 | 43.63 ± 0.18 | +17.96% |
| 1024 | 921.49 ± 8.38 | 617.24 ± 2.44 | +49.29% | 51.29 ± 0.17 | 43.10 ± 0.17 | +19.01% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
