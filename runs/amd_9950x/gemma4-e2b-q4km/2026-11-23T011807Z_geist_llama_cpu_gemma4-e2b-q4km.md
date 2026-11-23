# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a1751c84f0d4`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1367.62 ± 13.36 | 586.40 ± 2.52 | +133.22% | 51.39 ± 0.50 | 44.31 ± 0.08 | +15.98% |
| 256 | 1790.42 ± 16.37 | 617.37 ± 8.21 | +190.01% | 51.47 ± 0.10 | 43.73 ± 0.05 | +17.69% |
| 512 | 2132.87 ± 11.43 | 621.22 ± 9.50 | +243.34% | 51.38 ± 0.05 | 43.19 ± 0.08 | +18.96% |
| 1024 | 2323.14 ± 14.74 | 605.57 ± 2.88 | +283.63% | 51.25 ± 0.12 | 42.79 ± 0.14 | +19.77% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
