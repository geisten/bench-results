# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2609.42 ± 9.82 | 3733.64 ± 19.49 | -30.11% | 174.03 ± 0.10 | 194.27 ± 0.16 | -10.42% |
| 256 | 4070.86 ± 8.72 | 4178.09 ± 10.61 | -2.57% | 171.81 ± 0.24 | 185.77 ± 0.52 | -7.51% |
| 512 | 4921.07 ± 8.81 | 4736.82 ± 13.25 | +3.89% | 167.54 ± 0.13 | 182.44 ± 0.78 | -8.16% |
| 1024 | 4707.46 ± 3.02 | 4564.49 ± 4.48 | +3.13% | 165.34 ± 0.18 | 177.22 ± 0.12 | -6.71% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
