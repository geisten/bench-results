# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 964.85 ± 9.78 | 590.62 ± 2.37 | +63.36% | 51.94 ± 0.06 | 44.66 ± 0.07 | +16.31% |
| 256 | 965.88 ± 4.63 | 624.92 ± 3.43 | +54.56% | 51.78 ± 0.05 | 43.88 ± 0.09 | +18.02% |
| 512 | 955.06 ± 7.19 | 630.39 ± 2.13 | +51.50% | 51.52 ± 0.07 | 43.45 ± 0.03 | +18.58% |
| 1024 | 942.32 ± 3.30 | 614.41 ± 0.95 | +53.37% | 51.32 ± 0.05 | 43.07 ± 0.15 | +19.16% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
