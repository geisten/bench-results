# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 956.13 ± 5.59 | 593.97 ± 4.02 | +60.97% | 51.85 ± 0.05 | 44.58 ± 0.07 | +16.30% |
| 256 | 965.01 ± 9.81 | 626.50 ± 3.08 | +54.03% | 51.61 ± 0.07 | 43.95 ± 0.04 | +17.42% |
| 512 | 956.71 ± 2.91 | 633.17 ± 4.27 | +51.10% | 51.42 ± 0.16 | 43.42 ± 0.04 | +18.42% |
| 1024 | 938.69 ± 4.46 | 615.57 ± 5.40 | +52.49% | 51.16 ± 0.12 | 42.99 ± 0.12 | +18.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
