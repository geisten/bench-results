# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2570.80 ± 17.86 | 3810.05 ± 9.13 | -32.53% | 163.57 ± 0.34 | 173.39 ± 0.40 | -5.67% |
| 256 | 4088.32 ± 13.48 | 4664.48 ± 12.56 | -12.35% | 163.06 ± 0.27 | 166.50 ± 0.64 | -2.07% |
| 512 | 5756.30 ± 25.05 | 5139.05 ± 6.13 | +12.01% | 161.96 ± 0.16 | 165.24 ± 0.78 | -1.98% |
| 1024 | 5572.85 ± 7.85 | 4597.60 ± 10.45 | +21.21% | 161.37 ± 0.06 | 164.19 ± 0.51 | -1.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
