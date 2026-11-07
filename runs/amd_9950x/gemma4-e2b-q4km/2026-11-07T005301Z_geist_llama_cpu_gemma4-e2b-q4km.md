# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 678.53 ± 3.08 | 525.88 ± 1.91 | +29.03% | 51.19 ± 0.08 | 44.31 ± 0.04 | +15.52% |
| 256 | 680.35 ± 3.54 | 553.41 ± 2.44 | +22.94% | 50.86 ± 0.08 | 43.59 ± 0.05 | +16.69% |
| 512 | 682.48 ± 3.77 | 559.54 ± 2.04 | +21.97% | 50.68 ± 0.11 | 43.08 ± 0.04 | +17.63% |
| 1024 | 678.68 ± 2.65 | 542.44 ± 1.98 | +25.12% | 50.54 ± 0.12 | 42.75 ± 0.08 | +18.22% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
