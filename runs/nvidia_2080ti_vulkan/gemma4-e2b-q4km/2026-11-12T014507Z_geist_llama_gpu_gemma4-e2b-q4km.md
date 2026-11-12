# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2569.26 ± 10.32 | 3796.32 ± 7.59 | -32.32% | 163.33 ± 0.26 | 173.40 ± 0.28 | -5.81% |
| 256 | 4096.92 ± 6.80 | 4659.69 ± 11.66 | -12.08% | 162.77 ± 0.06 | 166.16 ± 0.46 | -2.04% |
| 512 | 5742.91 ± 25.20 | 5140.14 ± 7.04 | +11.73% | 161.80 ± 0.10 | 164.80 ± 0.56 | -1.82% |
| 1024 | 5564.34 ± 13.22 | 4591.86 ± 7.51 | +21.18% | 161.27 ± 0.09 | 163.90 ± 0.48 | -1.61% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
