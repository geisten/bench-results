# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b0ee998e552`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5146.56 ± 22.55 | 2247.49 ± 3.93 | +128.99% | 88.46 ± 0.07 | 84.37 ± 0.11 | +4.85% |
| 256 | 6856.93 ± 18.82 | 2852.06 ± 4.62 | +140.42% | 88.24 ± 0.04 | 84.12 ± 0.03 | +4.90% |
| 512 | 7588.90 ± 7.49 | 2801.45 ± 3.05 | +170.89% | 87.50 ± 0.04 | 83.60 ± 0.08 | +4.66% |
| 1024 | 7847.04 ± 6.79 | 2754.31 ± 1.49 | +184.90% | 87.03 ± 0.04 | 82.80 ± 0.09 | +5.11% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
