# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 668.77 ± 11.02 | 509.30 ± 1.63 | +31.31% | 48.33 ± 0.32 | 42.42 ± 0.28 | +13.93% |
| 256 | 671.14 ± 6.52 | 536.49 ± 1.64 | +25.10% | 48.14 ± 0.16 | 42.14 ± 0.56 | +14.23% |
| 512 | 669.47 ± 7.68 | 544.15 ± 1.22 | +23.03% | 47.97 ± 0.07 | 41.95 ± 0.18 | +14.36% |
| 1024 | 662.73 ± 7.65 | 522.17 ± 1.80 | +26.92% | 47.81 ± 0.06 | 40.99 ± 0.65 | +16.65% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
