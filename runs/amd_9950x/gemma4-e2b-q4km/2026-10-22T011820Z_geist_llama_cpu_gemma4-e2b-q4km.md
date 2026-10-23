# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f19377734f16`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 944.47 ± 10.45 | 587.56 ± 3.72 | +60.75% | 51.98 ± 0.18 | 44.51 ± 0.08 | +16.79% |
| 256 | 942.13 ± 5.89 | 620.09 ± 3.25 | +51.93% | 51.86 ± 0.14 | 43.63 ± 0.30 | +18.85% |
| 512 | 931.40 ± 10.36 | 626.84 ± 2.45 | +48.59% | 51.52 ± 0.19 | 43.23 ± 0.31 | +19.18% |
| 1024 | 922.96 ± 7.79 | 609.88 ± 2.00 | +51.34% | 51.52 ± 0.12 | 42.90 ± 0.15 | +20.08% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
