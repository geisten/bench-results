# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1025.01 ± 1.10 | 2280.24 ± 4.37 | -55.05% | 90.17 ± 0.07 | 87.42 ± 0.04 | +3.14% |
| 256 | 1040.74 ± 0.87 | 2877.97 ± 3.71 | -63.84% | 89.89 ± 0.05 | 87.06 ± 0.11 | +3.25% |
| 512 | 1034.50 ± 0.64 | 2820.87 ± 3.01 | -63.33% | 89.19 ± 0.04 | 86.65 ± 0.13 | +2.93% |
| 1024 | 1020.75 ± 0.68 | 2771.06 ± 2.26 | -63.16% | 88.65 ± 0.09 | 85.74 ± 0.22 | +3.39% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
