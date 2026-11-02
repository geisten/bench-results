# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f83e03b37679`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2594.61 ± 2.16 | 3819.85 ± 7.61 | -32.08% | 159.85 ± 0.26 | 173.45 ± 0.41 | -7.84% |
| 256 | 4092.30 ± 28.44 | 4679.57 ± 14.32 | -12.55% | 159.37 ± 0.36 | 166.36 ± 0.43 | -4.20% |
| 512 | 5754.81 ± 21.32 | 5163.08 ± 10.18 | +11.46% | 158.11 ± 0.27 | 165.28 ± 0.46 | -4.34% |
| 1024 | 5587.20 ± 10.79 | 4615.62 ± 13.36 | +21.05% | 157.16 ± 0.27 | 164.09 ± 0.21 | -4.22% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
