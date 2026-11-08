# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2621.66 ± 6.98 | 2285.35 ± 5.17 | +14.72% | 89.95 ± 0.04 | 86.48 ± 0.06 | +4.01% |
| 256 | 2721.16 ± 3.90 | 2881.03 ± 2.55 | -5.55% | 89.74 ± 0.02 | 86.17 ± 0.09 | +4.15% |
| 512 | 2702.12 ± 2.39 | 2822.75 ± 1.76 | -4.27% | 88.99 ± 0.06 | 85.51 ± 0.19 | +4.07% |
| 1024 | 2651.36 ± 3.12 | 2773.12 ± 2.89 | -4.39% | 88.39 ± 0.16 | 84.55 ± 0.16 | +4.54% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
