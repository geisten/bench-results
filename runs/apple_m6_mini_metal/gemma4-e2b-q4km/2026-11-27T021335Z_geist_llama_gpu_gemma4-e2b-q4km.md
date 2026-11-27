# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5209.92 ± 14.14 | 2275.68 ± 2.99 | +128.94% | 89.11 ± 0.03 | 84.78 ± 0.05 | +5.11% |
| 256 | 6921.91 ± 13.97 | 2879.57 ± 2.77 | +140.38% | 88.84 ± 0.01 | 84.52 ± 0.08 | +5.12% |
| 512 | 7669.03 ± 3.10 | 2824.78 ± 1.78 | +171.49% | 88.10 ± 0.03 | 84.07 ± 0.18 | +4.79% |
| 1024 | 7940.11 ± 4.13 | 2777.34 ± 0.58 | +185.89% | 87.62 ± 0.02 | 83.28 ± 0.18 | +5.20% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
