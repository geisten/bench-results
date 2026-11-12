# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 961.09 ± 6.51 | 592.92 ± 1.64 | +62.09% | 51.86 ± 0.08 | 44.54 ± 0.05 | +16.45% |
| 256 | 962.08 ± 6.63 | 624.37 ± 3.22 | +54.09% | 51.50 ± 0.06 | 43.87 ± 0.07 | +17.40% |
| 512 | 956.62 ± 3.31 | 630.93 ± 2.94 | +51.62% | 51.32 ± 0.08 | 43.41 ± 0.03 | +18.21% |
| 1024 | 939.22 ± 5.86 | 613.88 ± 2.34 | +53.00% | 51.14 ± 0.08 | 43.05 ± 0.03 | +18.79% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
