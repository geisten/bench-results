# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2608.70 ± 7.68 | 2259.08 ± 4.60 | +15.48% | 89.48 ± 0.04 | 85.90 ± 0.04 | +4.17% |
| 256 | 2696.58 ± 4.23 | 2861.89 ± 1.72 | -5.78% | 89.22 ± 0.03 | 85.57 ± 0.09 | +4.27% |
| 512 | 2678.95 ± 2.35 | 2807.61 ± 1.32 | -4.58% | 88.50 ± 0.03 | 85.05 ± 0.13 | +4.05% |
| 1024 | 2631.01 ± 2.09 | 2763.10 ± 2.24 | -4.78% | 87.97 ± 0.02 | 84.25 ± 0.10 | +4.42% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
