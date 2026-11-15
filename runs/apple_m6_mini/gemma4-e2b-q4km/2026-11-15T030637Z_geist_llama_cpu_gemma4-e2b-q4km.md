# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.24 ± 0.24 | 283.60 ± 0.07 | +27.38% | 71.39 ± 0.05 | 65.64 ± 0.07 | +8.76% |
| 256 | 354.23 ± 0.09 | 280.38 ± 0.36 | +26.34% | 69.37 ± 0.07 | 63.02 ± 0.11 | +10.08% |
| 512 | 340.88 ± 0.22 | 275.23 ± 0.35 | +23.85% | 65.86 ± 0.03 | 61.60 ± 0.16 | +6.92% |
| 1024 | 322.29 ± 0.09 | 260.72 ± 0.58 | +23.62% | 63.31 ± 0.03 | 59.69 ± 0.11 | +6.07% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
