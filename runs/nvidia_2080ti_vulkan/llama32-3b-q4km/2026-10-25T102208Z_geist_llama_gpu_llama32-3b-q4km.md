# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `d95bf356d2f7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on AMD Ryzen 9 9950X 16-Core Processor (RADV RAPHAEL_MENDOCINO), same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 21.24 ± 0.05 | 72.37 ± 0.02 | -70.64% | 8.60 ± 0.01 | 13.54 ± 0.03 | -36.51% |
| 256 | 20.19 ± 0.04 | 72.05 ± 0.13 | -71.97% | 8.74 ± 0.00 | 13.44 ± 0.03 | -34.99% |
| 512 | 18.20 ± 0.03 | 71.73 ± 0.06 | -74.63% | 8.47 ± 0.01 | 13.05 ± 0.02 | -35.09% |
| 1024 | 14.87 ± 0.02 | 70.65 ± 0.03 | -78.95% | 8.32 ± 0.01 | 12.78 ± 0.01 | -34.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
