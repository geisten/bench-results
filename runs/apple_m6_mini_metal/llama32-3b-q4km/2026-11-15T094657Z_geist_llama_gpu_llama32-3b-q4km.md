# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `9287d0c3734e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1983.71 ± 1.86 | 2093.72 ± 3.61 | -5.25% | 69.88 ± 0.01 | 69.59 ± 0.06 | +0.41% |
| 256 | 2070.94 ± 4.56 | 2224.10 ± 1.96 | -6.89% | 69.38 ± 0.02 | 69.25 ± 0.03 | +0.18% |
| 512 | 2060.13 ± 5.21 | 2139.09 ± 2.83 | -3.69% | 68.43 ± 0.02 | 68.22 ± 0.07 | +0.30% |
| 1024 | 2010.41 ± 2.72 | 2094.17 ± 1.16 | -4.00% | 66.60 ± 0.02 | 66.55 ± 0.03 | +0.09% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
