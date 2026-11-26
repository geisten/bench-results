# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5196.18 ± 13.96 | 2268.95 ± 5.34 | +129.01% | 89.01 ± 0.05 | 84.65 ± 0.06 | +5.16% |
| 256 | 6923.69 ± 5.80 | 2879.67 ± 3.85 | +140.43% | 88.74 ± 0.04 | 84.49 ± 0.11 | +5.04% |
| 512 | 7655.85 ± 6.59 | 2822.09 ± 2.80 | +171.28% | 87.98 ± 0.02 | 83.96 ± 0.10 | +4.79% |
| 1024 | 7926.52 ± 5.49 | 2775.14 ± 1.68 | +185.63% | 87.46 ± 0.05 | 83.21 ± 0.09 | +5.11% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
