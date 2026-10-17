# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b892b0f366c`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 683.21 ± 4.05 | 522.95 ± 2.08 | +30.64% | 51.27 ± 0.09 | 44.06 ± 0.08 | +16.35% |
| 256 | 690.64 ± 4.72 | 551.09 ± 1.90 | +25.32% | 50.95 ± 0.05 | 43.35 ± 0.07 | +17.52% |
| 512 | 689.12 ± 4.14 | 557.03 ± 0.59 | +23.71% | 50.84 ± 0.06 | 42.84 ± 0.05 | +18.67% |
| 1024 | 685.13 ± 4.00 | 542.06 ± 1.80 | +26.40% | 50.65 ± 0.05 | 42.52 ± 0.07 | +19.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
