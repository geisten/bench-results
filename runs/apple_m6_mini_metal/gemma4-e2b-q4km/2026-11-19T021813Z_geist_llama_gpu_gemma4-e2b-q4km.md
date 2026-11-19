# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2586.07 ± 8.77 | 2253.64 ± 5.62 | +14.75% | 88.37 ± 0.06 | 84.87 ± 0.09 | +4.13% |
| 256 | 2690.79 ± 3.32 | 2858.18 ± 4.11 | -5.86% | 88.19 ± 0.02 | 84.62 ± 0.04 | +4.22% |
| 512 | 2674.13 ± 3.45 | 2803.80 ± 1.75 | -4.62% | 87.49 ± 0.01 | 84.13 ± 0.06 | +3.99% |
| 1024 | 2627.49 ± 4.17 | 2759.37 ± 1.19 | -4.78% | 87.00 ± 0.07 | 83.30 ± 0.05 | +4.44% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
