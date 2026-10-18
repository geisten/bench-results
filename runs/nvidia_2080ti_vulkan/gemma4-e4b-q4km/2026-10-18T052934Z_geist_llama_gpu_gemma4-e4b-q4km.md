# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1555.65 ± 3.35 | 2369.12 ± 6.91 | -34.34% | 97.38 ± 0.04 | 104.12 ± 0.20 | -6.47% |
| 256 | 2554.88 ± 3.66 | 3034.45 ± 7.12 | -15.80% | 97.22 ± 0.09 | 103.71 ± 0.11 | -6.26% |
| 512 | 2945.39 ± 13.07 | 3039.34 ± 10.60 | -3.09% | 96.80 ± 0.11 | 102.92 ± 0.15 | -5.95% |
| 1024 | 2905.86 ± 3.05 | 2843.74 ± 5.17 | +2.18% | 96.45 ± 0.09 | 102.28 ± 0.13 | -5.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
