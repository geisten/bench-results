# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `1515c60147c9`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1556.89 ± 2.15 | 2365.74 ± 7.81 | -34.19% | 97.44 ± 0.03 | 104.13 ± 0.12 | -6.42% |
| 256 | 2554.24 ± 3.40 | 3037.18 ± 9.84 | -15.90% | 96.80 ± 0.03 | 103.74 ± 0.16 | -6.69% |
| 512 | 2946.83 ± 10.27 | 3035.85 ± 12.08 | -2.93% | 96.32 ± 0.05 | 103.01 ± 0.20 | -6.49% |
| 1024 | 2898.94 ± 4.76 | 2839.72 ± 9.82 | +2.09% | 96.01 ± 0.12 | 102.42 ± 0.09 | -6.26% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
