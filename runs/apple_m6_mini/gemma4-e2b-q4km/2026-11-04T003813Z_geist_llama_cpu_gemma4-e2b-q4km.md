# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `13cb783eddd2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.40 ± 0.16 | 283.69 ± 0.08 | +27.39% | 71.59 ± 0.08 | 65.78 ± 0.22 | +8.83% |
| 256 | 354.49 ± 0.23 | 280.36 ± 0.15 | +26.44% | 69.54 ± 0.05 | 63.29 ± 0.13 | +9.87% |
| 512 | 341.10 ± 0.30 | 275.35 ± 0.53 | +23.88% | 65.95 ± 0.05 | 61.98 ± 0.16 | +6.41% |
| 1024 | 322.55 ± 0.07 | 261.11 ± 0.47 | +23.53% | 63.40 ± 0.05 | 60.06 ± 0.09 | +5.57% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
