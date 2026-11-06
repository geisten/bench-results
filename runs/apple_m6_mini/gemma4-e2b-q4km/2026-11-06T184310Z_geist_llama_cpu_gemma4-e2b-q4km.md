# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.03 ± 0.51 | 283.69 ± 0.18 | +27.26% | 72.27 ± 0.11 | 66.33 ± 0.25 | +8.96% |
| 256 | 354.39 ± 0.25 | 280.21 ± 0.25 | +26.47% | 70.21 ± 0.07 | 63.80 ± 0.20 | +10.05% |
| 512 | 340.84 ± 0.33 | 275.46 ± 0.42 | +23.73% | 66.56 ± 0.09 | 62.30 ± 0.18 | +6.82% |
| 1024 | 321.57 ± 0.22 | 260.56 ± 0.67 | +23.41% | 64.02 ± 0.12 | 60.42 ± 0.11 | +5.96% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
