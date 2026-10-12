# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `4d6e2696a51b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 528.42 ± 1.94 | 590.79 ± 3.64 | -10.56% | 51.72 ± 0.15 | 44.41 ± 0.08 | +16.45% |
| 256 | 528.60 ± 1.78 | 622.84 ± 2.14 | -15.13% | 51.57 ± 0.12 | 43.55 ± 0.11 | +18.41% |
| 512 | 528.43 ± 1.54 | 628.91 ± 1.96 | -15.98% | 51.51 ± 0.13 | 43.14 ± 0.08 | +19.39% |
| 1024 | 524.71 ± 1.46 | 611.85 ± 3.06 | -14.24% | 51.40 ± 0.18 | 42.71 ± 0.09 | +20.34% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
