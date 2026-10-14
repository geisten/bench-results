# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `527bf29dd426`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 701.40 ± 5.15 | 585.64 ± 1.48 | +19.77% | 51.77 ± 0.09 | 44.21 ± 0.10 | +17.10% |
| 256 | 712.04 ± 4.82 | 619.48 ± 1.62 | +14.94% | 51.58 ± 0.05 | 43.65 ± 0.08 | +18.18% |
| 512 | 704.16 ± 2.05 | 626.90 ± 2.25 | +12.32% | 51.37 ± 0.10 | 43.19 ± 0.14 | +18.95% |
| 1024 | 698.92 ± 3.26 | 609.09 ± 1.82 | +14.75% | 51.17 ± 0.06 | 42.93 ± 0.12 | +19.19% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
