# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2640.10 ± 7.48 | 2276.28 ± 5.42 | +15.98% | 89.42 ± 0.04 | 85.86 ± 0.07 | +4.15% |
| 256 | 2725.84 ± 9.14 | 2878.55 ± 4.21 | -5.30% | 89.17 ± 0.02 | 85.54 ± 0.09 | +4.24% |
| 512 | 2713.13 ± 3.56 | 2824.71 ± 4.42 | -3.95% | 88.48 ± 0.08 | 85.00 ± 0.12 | +4.09% |
| 1024 | 2663.14 ± 3.47 | 2775.45 ± 3.66 | -4.05% | 87.89 ± 0.11 | 84.07 ± 0.14 | +4.54% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
