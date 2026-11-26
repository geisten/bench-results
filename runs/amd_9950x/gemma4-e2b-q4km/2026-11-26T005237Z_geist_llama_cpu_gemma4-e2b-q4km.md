# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1611.04 ± 25.37 | 587.99 ± 4.00 | +173.99% | 51.57 ± 0.16 | 44.36 ± 0.15 | +16.24% |
| 256 | 1664.32 ± 140.32 | 618.52 ± 1.22 | +169.08% | 51.21 ± 0.25 | 43.20 ± 0.64 | +18.54% |
| 512 | 2291.49 ± 12.79 | 622.57 ± 4.02 | +268.07% | 51.31 ± 0.10 | 43.23 ± 0.10 | +18.70% |
| 1024 | 2420.93 ± 10.81 | 606.77 ± 4.76 | +298.99% | 50.95 ± 0.12 | 42.78 ± 0.24 | +19.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
