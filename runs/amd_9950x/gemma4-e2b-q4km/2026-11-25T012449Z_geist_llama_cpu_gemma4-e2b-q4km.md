# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1362.01 ± 14.31 | 583.86 ± 6.85 | +133.28% | 51.65 ± 0.15 | 44.40 ± 0.18 | +16.33% |
| 256 | 1816.31 ± 11.15 | 619.16 ± 2.29 | +193.35% | 51.24 ± 0.14 | 43.75 ± 0.15 | +17.14% |
| 512 | 2150.26 ± 26.42 | 627.19 ± 2.60 | +242.84% | 51.08 ± 0.16 | 43.13 ± 0.34 | +18.45% |
| 1024 | 2339.36 ± 26.35 | 577.70 ± 29.69 | +304.95% | 50.95 ± 0.08 | 42.77 ± 0.28 | +19.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
