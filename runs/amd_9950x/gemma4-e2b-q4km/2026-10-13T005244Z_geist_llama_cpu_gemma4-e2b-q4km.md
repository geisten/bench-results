# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `db8314e2a3a3`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 527.43 ± 1.96 | 585.27 ± 3.40 | -9.88% | 51.88 ± 0.19 | 44.48 ± 0.11 | +16.62% |
| 256 | 529.12 ± 3.20 | 621.80 ± 4.84 | -14.90% | 51.84 ± 0.18 | 43.82 ± 0.07 | +18.32% |
| 512 | 526.28 ± 0.97 | 625.88 ± 3.83 | -15.91% | 51.58 ± 0.13 | 43.24 ± 0.12 | +19.30% |
| 1024 | 521.64 ± 1.57 | 608.37 ± 2.37 | -14.26% | 51.20 ± 0.21 | 42.81 ± 0.24 | +19.60% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
