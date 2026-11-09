# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 948.67 ± 9.86 | 599.10 ± 3.55 | +58.35% | 51.71 ± 0.09 | 44.55 ± 0.19 | +16.09% |
| 256 | 949.57 ± 12.08 | 627.44 ± 4.67 | +51.34% | 51.38 ± 0.17 | 43.69 ± 0.24 | +17.60% |
| 512 | 947.65 ± 2.30 | 634.97 ± 1.31 | +49.24% | 51.19 ± 0.12 | 43.49 ± 0.07 | +17.70% |
| 1024 | 929.89 ± 4.65 | 620.77 ± 2.29 | +49.80% | 51.05 ± 0.17 | 42.92 ± 0.22 | +18.95% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
