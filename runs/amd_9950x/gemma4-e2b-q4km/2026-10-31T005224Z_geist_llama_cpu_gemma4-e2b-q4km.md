# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 944.51 ± 9.62 | 596.18 ± 4.35 | +58.43% | 52.08 ± 0.11 | 44.85 ± 0.13 | +16.12% |
| 256 | 958.29 ± 3.74 | 625.03 ± 3.78 | +53.32% | 51.90 ± 0.05 | 44.05 ± 0.04 | +17.82% |
| 512 | 952.26 ± 4.86 | 634.70 ± 5.30 | +50.03% | 51.66 ± 0.04 | 43.52 ± 0.17 | +18.71% |
| 1024 | 929.95 ± 2.86 | 620.01 ± 2.92 | +49.99% | 51.37 ± 0.12 | 43.28 ± 0.10 | +18.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
