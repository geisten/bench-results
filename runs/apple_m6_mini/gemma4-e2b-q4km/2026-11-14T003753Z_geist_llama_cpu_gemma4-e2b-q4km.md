# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.13 ± 0.48 | 283.61 ± 0.09 | +27.33% | 72.26 ± 0.04 | 65.85 ± 0.32 | +9.74% |
| 256 | 354.38 ± 0.50 | 280.41 ± 0.25 | +26.38% | 70.11 ± 0.09 | 63.44 ± 0.27 | +10.52% |
| 512 | 340.82 ± 0.21 | 275.83 ± 0.41 | +23.56% | 66.51 ± 0.09 | 62.02 ± 0.26 | +7.24% |
| 1024 | 322.37 ± 0.26 | 260.96 ± 0.95 | +23.53% | 63.94 ± 0.05 | 60.00 ± 0.27 | +6.58% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
