# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `14ac9f78e1df`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 939.93 ± 11.15 | 589.21 ± 4.27 | +59.52% | 51.94 ± 0.22 | 44.41 ± 0.07 | +16.97% |
| 256 | 940.06 ± 5.94 | 621.60 ± 2.08 | +51.23% | 51.48 ± 0.18 | 43.82 ± 0.06 | +17.46% |
| 512 | 935.16 ± 9.48 | 625.90 ± 3.77 | +49.41% | 51.47 ± 0.07 | 43.31 ± 0.10 | +18.83% |
| 1024 | 921.93 ± 6.69 | 610.99 ± 1.30 | +50.89% | 51.19 ± 0.12 | 42.83 ± 0.16 | +19.53% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
