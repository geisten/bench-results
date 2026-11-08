# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1968.52 ± 2.76 | 2097.47 ± 2.31 | -6.15% | 69.94 ± 0.11 | 69.79 ± 0.08 | +0.21% |
| 256 | 2068.64 ± 6.25 | 2225.09 ± 0.98 | -7.03% | 69.46 ± 0.10 | 69.32 ± 0.11 | +0.19% |
| 512 | 2061.93 ± 2.00 | 2138.88 ± 1.74 | -3.60% | 68.61 ± 0.03 | 68.46 ± 0.05 | +0.23% |
| 1024 | 2008.91 ± 2.36 | 2093.52 ± 1.82 | -4.04% | 66.78 ± 0.03 | 66.81 ± 0.04 | -0.05% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
