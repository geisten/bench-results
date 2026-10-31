# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2570.90 ± 20.48 | 3727.96 ± 91.23 | -31.04% | 159.03 ± 0.52 | 173.56 ± 0.09 | -8.37% |
| 256 | 4094.23 ± 9.25 | 4657.90 ± 9.26 | -12.10% | 158.83 ± 0.38 | 166.55 ± 0.64 | -4.64% |
| 512 | 5758.82 ± 24.27 | 5143.33 ± 8.18 | +11.97% | 158.04 ± 0.23 | 165.61 ± 0.45 | -4.57% |
| 1024 | 5579.38 ± 10.84 | 4600.72 ± 15.88 | +21.27% | 157.70 ± 0.20 | 163.92 ± 0.48 | -3.79% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
