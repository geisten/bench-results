# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 544.67 ± 0.26 | 283.95 ± 0.10 | +91.82% | 72.21 ± 0.04 | 66.78 ± 0.07 | +8.13% |
| 256 | 714.75 ± 0.55 | 280.55 ± 0.29 | +154.77% | 70.10 ± 0.05 | 64.21 ± 0.07 | +9.16% |
| 512 | 823.29 ± 0.32 | 275.89 ± 0.91 | +198.41% | 66.51 ± 0.03 | 62.80 ± 0.05 | +5.90% |
| 1024 | 859.34 ± 0.58 | 261.20 ± 0.50 | +228.99% | 63.94 ± 0.04 | 60.77 ± 0.08 | +5.20% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
