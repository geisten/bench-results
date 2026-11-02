# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `e64ff1027649`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 361.50 ± 0.14 | 283.97 ± 0.05 | +27.30% | 70.97 ± 0.18 | 66.89 ± 0.04 | +6.10% |
| 256 | 357.49 ± 0.26 | 280.55 ± 0.18 | +27.43% | 69.00 ± 0.04 | 64.31 ± 0.02 | +7.29% |
| 512 | 341.09 ± 0.14 | 275.52 ± 0.67 | +23.80% | 65.46 ± 0.05 | 62.86 ± 0.03 | +4.15% |
| 1024 | 325.17 ± 0.28 | 260.88 ± 0.42 | +24.64% | 62.97 ± 0.09 | 60.86 ± 0.03 | +3.47% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
