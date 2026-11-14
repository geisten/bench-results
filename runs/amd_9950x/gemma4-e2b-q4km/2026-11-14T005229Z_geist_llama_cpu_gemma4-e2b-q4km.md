# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 963.92 ± 8.09 | 594.08 ± 2.78 | +62.26% | 51.76 ± 0.14 | 44.63 ± 0.06 | +15.97% |
| 256 | 951.47 ± 13.23 | 624.52 ± 2.52 | +52.35% | 51.74 ± 0.21 | 43.92 ± 0.08 | +17.81% |
| 512 | 954.15 ± 5.87 | 633.81 ± 2.90 | +50.54% | 51.47 ± 0.26 | 43.35 ± 0.07 | +18.73% |
| 1024 | 933.72 ± 4.87 | 614.48 ± 4.15 | +51.95% | 51.42 ± 0.20 | 43.04 ± 0.06 | +19.48% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
