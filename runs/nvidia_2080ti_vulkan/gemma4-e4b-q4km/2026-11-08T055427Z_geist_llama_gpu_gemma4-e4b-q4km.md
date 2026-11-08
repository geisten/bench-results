# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1556.89 ± 2.60 | 2370.22 ± 7.89 | -34.31% | 97.62 ± 0.13 | 104.37 ± 0.07 | -6.47% |
| 256 | 2551.10 ± 3.06 | 3032.75 ± 9.31 | -15.88% | 96.86 ± 0.08 | 103.54 ± 0.15 | -6.45% |
| 512 | 2946.40 ± 8.98 | 3041.20 ± 9.16 | -3.12% | 96.45 ± 0.03 | 103.00 ± 0.25 | -6.35% |
| 1024 | 2903.25 ± 3.53 | 2845.61 ± 6.17 | +2.03% | 96.17 ± 0.03 | 102.61 ± 0.20 | -6.28% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
