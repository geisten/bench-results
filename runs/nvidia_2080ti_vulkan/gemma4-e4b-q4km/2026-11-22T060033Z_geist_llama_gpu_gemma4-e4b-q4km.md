# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1555.08 ± 0.90 | 2363.95 ± 12.99 | -34.22% | 99.82 ± 0.08 | 103.99 ± 0.37 | -4.01% |
| 256 | 2555.00 ± 2.52 | 3031.36 ± 12.14 | -15.71% | 99.11 ± 0.08 | 104.07 ± 0.25 | -4.77% |
| 512 | 2939.01 ± 7.46 | 3037.10 ± 11.20 | -3.23% | 98.64 ± 0.09 | 102.79 ± 0.17 | -4.04% |
| 1024 | 2906.24 ± 1.64 | 2842.90 ± 6.79 | +2.23% | 98.27 ± 0.12 | 102.55 ± 0.22 | -4.18% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
