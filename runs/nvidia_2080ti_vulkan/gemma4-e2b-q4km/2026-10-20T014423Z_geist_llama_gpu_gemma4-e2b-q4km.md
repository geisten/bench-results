# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `44479afd263d`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2575.30 ± 10.30 | 3811.71 ± 5.97 | -32.44% | 158.82 ± 0.61 | 173.42 ± 0.46 | -8.42% |
| 256 | 4081.73 ± 13.52 | 4676.24 ± 16.49 | -12.71% | 159.36 ± 0.44 | 165.58 ± 0.49 | -3.76% |
| 512 | 5726.60 ± 24.91 | 5150.65 ± 15.46 | +11.18% | 158.07 ± 0.30 | 164.38 ± 0.44 | -3.84% |
| 1024 | 5572.65 ± 11.54 | 4621.31 ± 5.28 | +20.59% | 157.98 ± 0.47 | 163.53 ± 0.62 | -3.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
