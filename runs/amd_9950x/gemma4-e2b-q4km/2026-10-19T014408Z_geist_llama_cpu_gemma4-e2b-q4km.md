# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `2b5263f87833`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 682.49 ± 6.24 | 524.12 ± 2.92 | +30.22% | 50.83 ± 0.21 | 43.90 ± 0.16 | +15.79% |
| 256 | 686.38 ± 5.05 | 553.48 ± 1.79 | +24.01% | 50.76 ± 0.17 | 43.26 ± 0.07 | +17.35% |
| 512 | 687.39 ± 4.72 | 558.04 ± 1.05 | +23.18% | 50.78 ± 0.07 | 42.71 ± 0.13 | +18.88% |
| 1024 | 685.23 ± 1.53 | 541.36 ± 1.29 | +26.57% | 50.58 ± 0.12 | 42.43 ± 0.12 | +19.21% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
