# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `406a3c0519ec`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 951.45 ± 9.38 | 592.96 ± 1.74 | +60.46% | 51.81 ± 0.12 | 44.38 ± 0.16 | +16.74% |
| 256 | 957.99 ± 11.27 | 625.14 ± 3.10 | +53.24% | 51.60 ± 0.12 | 43.71 ± 0.14 | +18.04% |
| 512 | 947.70 ± 3.80 | 632.39 ± 1.57 | +49.86% | 51.44 ± 0.10 | 43.18 ± 0.19 | +19.13% |
| 1024 | 932.37 ± 3.91 | 616.67 ± 1.08 | +51.20% | 51.32 ± 0.07 | 42.91 ± 0.08 | +19.60% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
