# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2570.80 ± 14.71 | 3792.24 ± 17.82 | -32.21% | 163.53 ± 0.43 | 173.33 ± 0.25 | -5.65% |
| 256 | 4090.54 ± 5.75 | 4663.21 ± 21.93 | -12.28% | 162.84 ± 0.14 | 166.44 ± 0.45 | -2.16% |
| 512 | 5751.97 ± 12.43 | 5147.15 ± 10.46 | +11.75% | 161.85 ± 0.06 | 165.15 ± 0.31 | -2.00% |
| 1024 | 5570.43 ± 9.55 | 4602.73 ± 9.45 | +21.02% | 161.39 ± 0.03 | 163.85 ± 0.66 | -1.50% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
