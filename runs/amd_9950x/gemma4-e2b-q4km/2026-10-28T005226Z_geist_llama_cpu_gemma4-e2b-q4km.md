# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `13921becb240`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 959.52 ± 4.50 | 591.68 ± 3.50 | +62.17% | 51.91 ± 0.10 | 44.56 ± 0.06 | +16.51% |
| 256 | 960.24 ± 8.39 | 625.59 ± 2.85 | +53.49% | 51.73 ± 0.10 | 43.72 ± 0.07 | +18.31% |
| 512 | 948.82 ± 5.69 | 632.38 ± 2.49 | +50.04% | 51.57 ± 0.13 | 43.23 ± 0.11 | +19.28% |
| 1024 | 936.27 ± 4.03 | 614.86 ± 2.46 | +52.27% | 51.39 ± 0.13 | 43.00 ± 0.09 | +19.51% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
