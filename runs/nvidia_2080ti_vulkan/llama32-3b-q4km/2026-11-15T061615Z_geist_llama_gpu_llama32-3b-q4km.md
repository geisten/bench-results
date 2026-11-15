# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2615.80 ± 12.66 | 3738.96 ± 17.12 | -30.04% | 173.01 ± 0.28 | 191.95 ± 0.31 | -9.87% |
| 256 | 4055.80 ± 10.96 | 4174.87 ± 6.11 | -2.85% | 170.97 ± 0.07 | 185.14 ± 0.34 | -7.65% |
| 512 | 4905.95 ± 9.09 | 4729.15 ± 10.01 | +3.74% | 166.77 ± 0.16 | 182.51 ± 0.82 | -8.62% |
| 1024 | 4696.70 ± 3.18 | 4566.07 ± 7.87 | +2.86% | 164.52 ± 0.13 | 179.71 ± 0.06 | -8.45% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
