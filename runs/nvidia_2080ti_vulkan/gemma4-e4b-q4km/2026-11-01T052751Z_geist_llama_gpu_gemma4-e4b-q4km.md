# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1560.12 ± 2.29 | 2374.78 ± 8.82 | -34.30% | 97.87 ± 0.17 | 104.32 ± 0.18 | -6.19% |
| 256 | 2555.17 ± 2.28 | 3038.38 ± 11.94 | -15.90% | 97.29 ± 0.07 | 103.89 ± 0.34 | -6.35% |
| 512 | 2944.15 ± 15.52 | 3039.96 ± 11.77 | -3.15% | 96.85 ± 0.05 | 103.30 ± 0.30 | -6.24% |
| 1024 | 2906.72 ± 2.45 | 2854.55 ± 4.07 | +1.83% | 96.50 ± 0.04 | 102.74 ± 0.18 | -6.07% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
