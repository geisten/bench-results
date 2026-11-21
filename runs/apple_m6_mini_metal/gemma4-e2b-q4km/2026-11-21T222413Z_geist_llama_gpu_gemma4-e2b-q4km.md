# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2589.26 ± 11.90 | 2254.33 ± 11.21 | +14.86% | 88.28 ± 0.08 | 84.69 ± 0.07 | +4.23% |
| 256 | 2689.01 ± 2.28 | 2856.64 ± 2.97 | -5.87% | 88.08 ± 0.03 | 84.35 ± 0.07 | +4.42% |
| 512 | 2672.02 ± 0.77 | 2800.13 ± 1.31 | -4.57% | 87.34 ± 0.02 | 83.94 ± 0.05 | +4.04% |
| 1024 | 2624.88 ± 1.98 | 2752.61 ± 1.09 | -4.64% | 86.83 ± 0.03 | 83.06 ± 0.07 | +4.54% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
