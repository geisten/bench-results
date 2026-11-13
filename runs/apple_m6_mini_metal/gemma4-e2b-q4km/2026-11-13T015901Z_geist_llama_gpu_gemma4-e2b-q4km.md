# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2639.72 ± 8.13 | 2282.66 ± 3.88 | +15.64% | 89.57 ± 0.09 | 85.99 ± 0.04 | +4.16% |
| 256 | 2725.87 ± 6.14 | 2880.03 ± 2.06 | -5.35% | 89.35 ± 0.03 | 85.72 ± 0.09 | +4.24% |
| 512 | 2710.54 ± 3.08 | 2828.25 ± 1.98 | -4.16% | 88.63 ± 0.02 | 85.22 ± 0.06 | +3.99% |
| 1024 | 2663.83 ± 1.29 | 2777.01 ± 2.16 | -4.08% | 88.12 ± 0.03 | 84.31 ± 0.12 | +4.52% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
