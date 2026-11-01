# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2629.58 ± 3.70 | 2278.36 ± 3.29 | +15.42% | 90.41 ± 0.02 | 87.73 ± 0.08 | +3.06% |
| 256 | 2718.14 ± 3.28 | 2883.55 ± 2.47 | -5.74% | 90.15 ± 0.02 | 87.43 ± 0.11 | +3.11% |
| 512 | 2699.33 ± 1.58 | 2827.53 ± 1.58 | -4.53% | 89.42 ± 0.02 | 86.98 ± 0.09 | +2.80% |
| 1024 | 2649.78 ± 0.94 | 2779.38 ± 2.26 | -4.66% | 88.91 ± 0.03 | 86.10 ± 0.12 | +3.27% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
