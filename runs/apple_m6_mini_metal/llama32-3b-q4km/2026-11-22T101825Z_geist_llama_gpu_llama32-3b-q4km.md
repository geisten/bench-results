# Current GPU head-to-head: geist vs llama.cpp

Model: `llama-3.2-3b-Q4_K_M.gguf` (`6c1a2b41161032677be168d354123594c0e6e67d2b9227c84f296ad037c728ff`)

geist `7765ee2a075d`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1962.54 ± 3.76 | 2089.81 ± 3.30 | -6.09% | 69.41 ± 0.02 | 69.12 ± 0.06 | +0.42% |
| 256 | 2045.45 ± 2.19 | 2213.31 ± 4.49 | -7.58% | 68.96 ± 0.04 | 68.73 ± 0.04 | +0.33% |
| 512 | 2039.20 ± 2.96 | 2130.49 ± 1.34 | -4.29% | 68.00 ± 0.02 | 67.75 ± 0.06 | +0.37% |
| 1024 | 1988.02 ± 3.04 | 2082.86 ± 2.47 | -4.55% | 66.14 ± 0.02 | 66.16 ± 0.02 | -0.02% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
