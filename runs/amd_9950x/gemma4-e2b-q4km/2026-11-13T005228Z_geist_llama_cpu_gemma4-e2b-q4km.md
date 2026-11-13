# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 958.29 ± 8.42 | 593.29 ± 2.27 | +61.52% | 51.81 ± 0.08 | 44.64 ± 0.11 | +16.08% |
| 256 | 958.09 ± 7.70 | 623.37 ± 3.44 | +53.69% | 51.56 ± 0.10 | 43.92 ± 0.08 | +17.40% |
| 512 | 955.55 ± 8.88 | 629.32 ± 2.13 | +51.84% | 51.54 ± 0.12 | 43.42 ± 0.07 | +18.69% |
| 1024 | 937.18 ± 7.68 | 614.75 ± 1.74 | +52.45% | 51.43 ± 0.09 | 43.01 ± 0.08 | +19.59% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
