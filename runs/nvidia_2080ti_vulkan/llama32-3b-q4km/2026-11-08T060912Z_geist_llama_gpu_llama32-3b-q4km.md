# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2616.34 ± 14.96 | 3732.26 ± 10.00 | -29.90% | 156.34 ± 0.07 | 192.03 ± 0.29 | -18.59% |
| 256 | 4065.40 ± 21.54 | 4166.44 ± 17.91 | -2.43% | 154.22 ± 0.11 | 184.30 ± 0.68 | -16.32% |
| 512 | 4875.26 ± 12.22 | 4728.68 ± 8.87 | +3.10% | 150.67 ± 0.05 | 182.17 ± 0.52 | -17.29% |
| 1024 | 4690.56 ± 7.69 | 4562.10 ± 9.35 | +2.82% | 148.89 ± 0.03 | 179.60 ± 0.83 | -17.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
