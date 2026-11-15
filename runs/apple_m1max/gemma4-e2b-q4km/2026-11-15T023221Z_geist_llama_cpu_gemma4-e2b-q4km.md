# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 351.90 ± 0.24 | 308.91 ± 0.16 | +13.92% | 63.37 ± 0.09 | 51.12 ± 0.21 | +23.96% |
| 256 | 345.93 ± 0.30 | 315.33 ± 2.12 | +9.70% | 61.04 ± 0.08 | 49.60 ± 0.24 | +23.06% |
| 512 | 332.87 ± 0.91 | 306.47 ± 4.01 | +8.62% | 57.01 ± 0.18 | 48.69 ± 0.20 | +17.08% |
| 1024 | 304.54 ± 3.97 | 293.23 ± 5.83 | +3.86% | 54.30 ± 0.21 | 47.91 ± 0.35 | +13.35% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
