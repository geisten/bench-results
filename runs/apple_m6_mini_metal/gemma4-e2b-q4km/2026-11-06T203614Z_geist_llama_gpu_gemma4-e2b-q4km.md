# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2622.82 ± 3.98 | 2285.36 ± 2.22 | +14.77% | 89.73 ± 0.07 | 85.72 ± 0.20 | +4.67% |
| 256 | 2715.59 ± 3.65 | 2881.97 ± 2.99 | -5.77% | 89.39 ± 0.09 | 85.40 ± 0.13 | +4.67% |
| 512 | 2697.44 ± 2.11 | 2829.95 ± 2.72 | -4.68% | 88.69 ± 0.06 | 84.93 ± 0.23 | +4.42% |
| 1024 | 2649.28 ± 1.87 | 2783.36 ± 2.25 | -4.82% | 88.21 ± 0.03 | 84.16 ± 0.11 | +4.81% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
