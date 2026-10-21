# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `24515004c598`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 685.28 ± 6.88 | 524.38 ± 0.71 | +30.69% | 51.12 ± 0.12 | 44.05 ± 0.06 | +16.05% |
| 256 | 687.37 ± 4.77 | 549.64 ± 3.21 | +25.06% | 50.90 ± 0.12 | 43.35 ± 0.07 | +17.40% |
| 512 | 686.93 ± 4.69 | 555.91 ± 2.65 | +23.57% | 50.74 ± 0.14 | 42.92 ± 0.09 | +18.22% |
| 1024 | 684.85 ± 5.36 | 541.30 ± 2.64 | +26.52% | 50.62 ± 0.12 | 42.50 ± 0.15 | +19.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
