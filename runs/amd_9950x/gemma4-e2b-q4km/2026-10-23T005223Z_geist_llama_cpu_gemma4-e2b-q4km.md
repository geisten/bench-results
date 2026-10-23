# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `cdc4ba43c58a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 932.88 ± 16.03 | 584.60 ± 3.24 | +59.58% | 51.56 ± 0.37 | 44.35 ± 0.10 | +16.25% |
| 256 | 947.51 ± 4.63 | 617.54 ± 3.83 | +53.43% | 51.57 ± 0.04 | 43.60 ± 0.21 | +18.28% |
| 512 | 933.47 ± 4.21 | 628.90 ± 1.30 | +48.43% | 51.40 ± 0.13 | 43.34 ± 0.15 | +18.61% |
| 1024 | 923.52 ± 6.42 | 610.66 ± 0.84 | +51.23% | 50.99 ± 0.12 | 42.86 ± 0.16 | +18.97% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
