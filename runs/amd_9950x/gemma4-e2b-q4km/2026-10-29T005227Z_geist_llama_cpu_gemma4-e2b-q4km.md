# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `c212773b0268`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 955.06 ± 9.34 | 595.22 ± 1.17 | +60.45% | 52.01 ± 0.04 | 44.59 ± 0.06 | +16.65% |
| 256 | 965.84 ± 3.51 | 626.08 ± 1.90 | +54.27% | 51.78 ± 0.04 | 43.82 ± 0.17 | +18.16% |
| 512 | 951.13 ± 3.32 | 635.56 ± 1.77 | +49.65% | 51.58 ± 0.08 | 43.37 ± 0.06 | +18.93% |
| 1024 | 936.77 ± 1.99 | 616.03 ± 1.67 | +52.07% | 51.40 ± 0.05 | 42.99 ± 0.13 | +19.55% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
