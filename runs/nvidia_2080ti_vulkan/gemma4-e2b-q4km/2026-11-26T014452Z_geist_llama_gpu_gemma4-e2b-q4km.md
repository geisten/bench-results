# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2590.25 ± 2.73 | 3813.47 ± 6.28 | -32.08% | 164.75 ± 0.39 | 174.86 ± 0.11 | -5.78% |
| 256 | 4110.55 ± 11.37 | 4668.27 ± 9.28 | -11.95% | 164.41 ± 0.32 | 166.31 ± 1.08 | -1.14% |
| 512 | 5738.85 ± 18.87 | 5155.05 ± 7.65 | +11.32% | 163.56 ± 0.26 | 165.10 ± 0.78 | -0.93% |
| 1024 | 8111.73 ± 18.21 | 4611.94 ± 5.81 | +75.89% | 162.76 ± 0.23 | 164.33 ± 0.90 | -0.96% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
