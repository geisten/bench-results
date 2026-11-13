# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 360.96 ± 0.28 | 283.65 ± 0.10 | +27.26% | 72.48 ± 0.06 | 65.83 ± 0.15 | +10.11% |
| 256 | 356.28 ± 1.55 | 280.28 ± 0.27 | +27.12% | 70.37 ± 0.09 | 63.39 ± 0.16 | +11.00% |
| 512 | 340.73 ± 0.25 | 275.49 ± 0.46 | +23.68% | 66.70 ± 0.08 | 62.03 ± 0.18 | +7.53% |
| 1024 | 322.15 ± 0.40 | 260.83 ± 0.88 | +23.51% | 64.04 ± 0.14 | 60.04 ± 0.15 | +6.67% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
