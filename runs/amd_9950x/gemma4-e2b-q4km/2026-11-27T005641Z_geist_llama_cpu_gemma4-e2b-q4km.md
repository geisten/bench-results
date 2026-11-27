# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1503.01 ± 117.90 | 582.18 ± 9.51 | +158.17% | 50.34 ± 1.20 | 43.26 ± 1.12 | +16.35% |
| 256 | 2019.92 ± 36.23 | 621.30 ± 4.75 | +225.11% | 51.24 ± 0.28 | 43.02 ± 0.64 | +19.11% |
| 512 | 2296.94 ± 14.45 | 624.42 ± 3.95 | +267.85% | 51.20 ± 0.15 | 42.98 ± 0.17 | +19.11% |
| 1024 | 2422.13 ± 26.39 | 608.47 ± 3.01 | +298.07% | 51.15 ± 0.14 | 42.08 ± 0.93 | +21.54% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
