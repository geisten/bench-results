# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5145.63 ± 10.36 | 2275.22 ± 3.05 | +126.16% | 89.45 ± 0.04 | 85.21 ± 0.03 | +4.97% |
| 256 | 6499.28 ± 12.95 | 2880.69 ± 1.77 | +125.61% | 89.17 ± 0.02 | 84.94 ± 0.11 | +4.98% |
| 512 | 7149.04 ± 3.84 | 2829.85 ± 2.05 | +152.63% | 88.44 ± 0.04 | 84.56 ± 0.05 | +4.60% |
| 1024 | 7385.53 ± 3.54 | 2773.85 ± 1.43 | +166.26% | 87.93 ± 0.03 | 83.74 ± 0.09 | +5.00% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
