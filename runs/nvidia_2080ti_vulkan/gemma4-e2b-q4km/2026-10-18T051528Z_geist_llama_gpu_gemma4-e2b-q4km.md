# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2572.09 ± 15.00 | 3785.50 ± 37.10 | -32.05% | 158.60 ± 0.18 | 173.35 ± 0.39 | -8.51% |
| 256 | 4099.45 ± 13.00 | 4668.18 ± 14.47 | -12.18% | 159.31 ± 0.06 | 165.86 ± 0.36 | -3.95% |
| 512 | 5749.42 ± 11.63 | 5142.47 ± 12.97 | +11.80% | 158.22 ± 0.25 | 164.67 ± 0.43 | -3.92% |
| 1024 | 5575.25 ± 10.32 | 4605.31 ± 10.62 | +21.06% | 157.90 ± 0.29 | 163.63 ± 0.64 | -3.50% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
