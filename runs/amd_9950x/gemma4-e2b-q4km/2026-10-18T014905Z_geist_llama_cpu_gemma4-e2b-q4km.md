# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 954.34 ± 14.33 | 590.27 ± 2.86 | +61.68% | 51.69 ± 0.34 | 44.53 ± 0.19 | +16.08% |
| 256 | 956.33 ± 7.44 | 621.78 ± 2.01 | +53.80% | 51.63 ± 0.16 | 43.74 ± 0.16 | +18.02% |
| 512 | 948.51 ± 9.16 | 627.54 ± 2.47 | +51.15% | 51.62 ± 0.08 | 43.41 ± 0.08 | +18.92% |
| 1024 | 926.76 ± 3.11 | 611.62 ± 1.57 | +51.53% | 51.36 ± 0.09 | 42.91 ± 0.22 | +19.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
