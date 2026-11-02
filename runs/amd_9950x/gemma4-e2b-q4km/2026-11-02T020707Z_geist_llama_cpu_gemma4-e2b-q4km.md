# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `e64ff1027649`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 959.93 ± 10.60 | 589.22 ± 10.44 | +62.92% | 51.86 ± 0.29 | 44.34 ± 0.13 | +16.97% |
| 256 | 957.84 ± 10.68 | 629.57 ± 2.00 | +52.14% | 51.55 ± 0.24 | 43.73 ± 0.05 | +17.89% |
| 512 | 949.04 ± 17.31 | 635.66 ± 3.03 | +49.30% | 51.44 ± 0.28 | 43.28 ± 0.16 | +18.84% |
| 1024 | 932.44 ± 5.73 | 616.47 ± 3.88 | +51.26% | 51.27 ± 0.15 | 43.01 ± 0.13 | +19.21% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
