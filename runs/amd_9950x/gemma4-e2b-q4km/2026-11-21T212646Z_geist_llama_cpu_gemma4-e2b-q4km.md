# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 940.95 ± 15.53 | 587.37 ± 3.03 | +60.20% | 51.75 ± 0.12 | 44.61 ± 0.12 | +16.00% |
| 256 | 940.59 ± 5.41 | 618.21 ± 5.29 | +52.15% | 51.65 ± 0.06 | 43.92 ± 0.11 | +17.61% |
| 512 | 929.04 ± 7.66 | 620.14 ± 5.10 | +49.81% | 51.49 ± 0.11 | 43.55 ± 0.10 | +18.24% |
| 1024 | 915.78 ± 4.83 | 604.96 ± 3.80 | +51.38% | 51.16 ± 0.13 | 42.94 ± 0.13 | +19.16% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
