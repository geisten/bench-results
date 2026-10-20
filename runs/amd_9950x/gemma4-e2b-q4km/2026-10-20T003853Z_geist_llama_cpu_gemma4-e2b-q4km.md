# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `44479afd263d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 688.63 ± 8.55 | 524.48 ± 1.14 | +31.30% | 50.96 ± 0.20 | 43.90 ± 0.10 | +16.08% |
| 256 | 681.49 ± 3.53 | 551.43 ± 0.72 | +23.59% | 50.64 ± 0.23 | 43.19 ± 0.03 | +17.24% |
| 512 | 681.09 ± 4.43 | 556.84 ± 1.27 | +22.31% | 50.48 ± 0.11 | 42.72 ± 0.07 | +18.18% |
| 1024 | 679.15 ± 4.04 | 542.00 ± 0.75 | +25.31% | 50.38 ± 0.07 | 42.28 ± 0.10 | +19.17% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
