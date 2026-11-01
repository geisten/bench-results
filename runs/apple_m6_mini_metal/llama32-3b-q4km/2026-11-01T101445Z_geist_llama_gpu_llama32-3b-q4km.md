# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1979.85 ± 1.64 | 2101.47 ± 3.64 | -5.79% | 70.42 ± 0.01 | 70.42 ± 0.03 | -0.00% |
| 256 | 2076.67 ± 2.05 | 2224.46 ± 0.85 | -6.64% | 69.90 ± 0.01 | 69.99 ± 0.06 | -0.14% |
| 512 | 2067.16 ± 1.47 | 2138.35 ± 3.78 | -3.33% | 69.00 ± 0.02 | 68.81 ± 0.05 | +0.28% |
| 1024 | 2013.14 ± 2.75 | 2094.49 ± 2.95 | -3.88% | 67.13 ± 0.04 | 67.29 ± 0.05 | -0.23% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
