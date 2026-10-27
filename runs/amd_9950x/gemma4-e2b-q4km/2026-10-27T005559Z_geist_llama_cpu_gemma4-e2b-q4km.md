# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `df665fe9c736`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 668.88 ± 4.02 | 514.77 ± 1.12 | +29.94% | 49.59 ± 0.69 | 42.96 ± 0.13 | +15.45% |
| 256 | 676.04 ± 4.52 | 541.53 ± 0.58 | +24.84% | 48.79 ± 1.32 | 42.11 ± 0.10 | +15.87% |
| 512 | 670.68 ± 6.90 | 548.74 ± 2.86 | +22.22% | 49.13 ± 0.84 | 42.24 ± 0.37 | +16.31% |
| 1024 | 662.12 ± 5.45 | 530.95 ± 1.24 | +24.70% | 48.93 ± 0.83 | 42.13 ± 0.13 | +16.14% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
