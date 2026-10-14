# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `db8314e2a3a3`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2581.40 ± 7.78 | 3807.14 ± 12.87 | -32.20% | 158.37 ± 0.20 | 166.65 ± 0.45 | -4.97% |
| 256 | 4102.01 ± 7.19 | 4685.99 ± 16.22 | -12.46% | 158.88 ± 0.08 | 166.55 ± 0.30 | -4.61% |
| 512 | 5766.87 ± 11.72 | 5152.98 ± 7.14 | +11.91% | 158.01 ± 0.05 | 165.26 ± 0.46 | -4.39% |
| 1024 | 5595.28 ± 7.76 | 4625.92 ± 12.41 | +20.95% | 157.55 ± 0.06 | 164.45 ± 0.59 | -4.19% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
