# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `ebcdfb017ba6`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 950.58 ± 8.67 | 590.05 ± 3.41 | +61.10% | 51.69 ± 0.15 | 44.38 ± 0.20 | +16.46% |
| 256 | 955.69 ± 2.72 | 624.30 ± 0.91 | +53.08% | 51.79 ± 0.13 | 43.73 ± 0.11 | +18.42% |
| 512 | 942.30 ± 4.48 | 630.40 ± 3.11 | +49.48% | 51.65 ± 0.08 | 43.12 ± 0.20 | +19.78% |
| 1024 | 926.91 ± 5.87 | 611.46 ± 2.12 | +51.59% | 51.06 ± 0.20 | 42.85 ± 0.09 | +19.15% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
