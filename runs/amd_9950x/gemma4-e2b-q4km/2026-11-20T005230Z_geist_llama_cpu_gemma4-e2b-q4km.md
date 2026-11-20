# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 949.13 ± 6.34 | 587.14 ± 2.72 | +61.65% | 51.70 ± 0.09 | 44.54 ± 0.08 | +16.08% |
| 256 | 942.98 ± 6.90 | 620.39 ± 3.63 | +52.00% | 51.43 ± 0.06 | 43.81 ± 0.10 | +17.40% |
| 512 | 939.20 ± 4.81 | 622.00 ± 6.71 | +51.00% | 51.26 ± 0.09 | 43.33 ± 0.07 | +18.31% |
| 1024 | 919.61 ± 7.59 | 611.67 ± 3.67 | +50.34% | 51.19 ± 0.10 | 43.02 ± 0.14 | +18.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
