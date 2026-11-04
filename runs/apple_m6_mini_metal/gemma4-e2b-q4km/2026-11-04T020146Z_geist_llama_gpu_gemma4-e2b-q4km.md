# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2626.75 ± 4.71 | 2289.88 ± 1.68 | +14.71% | 90.68 ± 0.04 | 87.86 ± 0.10 | +3.21% |
| 256 | 2720.64 ± 3.60 | 2883.30 ± 2.28 | -5.64% | 90.42 ± 0.03 | 87.60 ± 0.08 | +3.22% |
| 512 | 2700.81 ± 3.23 | 2829.20 ± 2.80 | -4.54% | 89.70 ± 0.02 | 87.19 ± 0.05 | +2.88% |
| 1024 | 2652.28 ± 2.16 | 2779.02 ± 1.47 | -4.56% | 89.17 ± 0.03 | 86.39 ± 0.06 | +3.21% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
