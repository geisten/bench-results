# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2625.26 ± 5.53 | 2278.02 ± 2.74 | +15.24% | 90.11 ± 0.01 | 87.19 ± 0.10 | +3.35% |
| 256 | 2716.41 ± 3.60 | 2882.23 ± 1.32 | -5.75% | 89.82 ± 0.02 | 87.00 ± 0.07 | +3.24% |
| 512 | 2697.18 ± 2.36 | 2828.41 ± 2.09 | -4.64% | 89.13 ± 0.02 | 86.47 ± 0.11 | +3.07% |
| 1024 | 2650.31 ± 2.02 | 2774.77 ± 1.66 | -4.49% | 88.62 ± 0.02 | 85.68 ± 0.15 | +3.44% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
