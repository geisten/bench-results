# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 682.22 ± 3.87 | 523.73 ± 0.87 | +30.26% | 51.16 ± 0.05 | 44.21 ± 0.04 | +15.72% |
| 256 | 689.32 ± 3.72 | 548.88 ± 1.64 | +25.58% | 50.90 ± 0.07 | 43.41 ± 0.04 | +17.26% |
| 512 | 685.95 ± 6.45 | 555.16 ± 0.99 | +23.56% | 50.69 ± 0.05 | 42.99 ± 0.04 | +17.92% |
| 1024 | 682.07 ± 5.89 | 539.28 ± 1.12 | +26.48% | 50.50 ± 0.09 | 42.55 ± 0.06 | +18.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
