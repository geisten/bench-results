# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `eedaae6cae7b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 961.66 ± 14.55 | 592.91 ± 2.04 | +62.19% | 51.87 ± 0.06 | 44.74 ± 0.08 | +15.94% |
| 256 | 962.62 ± 11.28 | 626.89 ± 2.42 | +53.55% | 51.59 ± 0.04 | 43.94 ± 0.08 | +17.40% |
| 512 | 945.79 ± 11.90 | 634.83 ± 2.16 | +48.98% | 51.33 ± 0.07 | 43.32 ± 0.17 | +18.51% |
| 1024 | 936.80 ± 4.91 | 616.86 ± 2.88 | +51.87% | 51.23 ± 0.12 | 42.82 ± 0.10 | +19.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
