# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 966.76 ± 4.43 | 590.36 ± 2.12 | +63.76% | 51.74 ± 0.15 | 44.47 ± 0.11 | +16.34% |
| 256 | 963.95 ± 2.38 | 623.28 ± 2.56 | +54.66% | 51.40 ± 0.12 | 43.80 ± 0.09 | +17.35% |
| 512 | 951.42 ± 4.07 | 629.24 ± 3.96 | +51.20% | 51.18 ± 0.14 | 43.23 ± 0.08 | +18.38% |
| 1024 | 937.32 ± 1.38 | 612.68 ± 4.13 | +52.99% | 51.01 ± 0.08 | 42.96 ± 0.09 | +18.73% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
