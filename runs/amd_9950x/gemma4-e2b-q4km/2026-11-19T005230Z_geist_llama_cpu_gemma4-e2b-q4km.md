# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 948.18 ± 6.37 | 588.53 ± 3.78 | +61.11% | 51.74 ± 0.21 | 44.42 ± 0.04 | +16.47% |
| 256 | 941.78 ± 3.90 | 621.57 ± 1.70 | +51.52% | 51.58 ± 0.41 | 43.72 ± 0.12 | +17.99% |
| 512 | 931.83 ± 5.40 | 622.77 ± 7.47 | +49.63% | 51.46 ± 0.22 | 43.24 ± 0.18 | +19.01% |
| 1024 | 917.25 ± 3.75 | 611.38 ± 2.00 | +50.03% | 51.19 ± 0.17 | 42.86 ± 0.10 | +19.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
