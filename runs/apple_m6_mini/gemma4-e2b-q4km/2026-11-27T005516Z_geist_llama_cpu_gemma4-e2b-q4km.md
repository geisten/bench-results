# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 940.65 ± 0.78 | 283.84 ± 0.06 | +231.40% | 72.17 ± 0.05 | 66.85 ± 0.07 | +7.96% |
| 256 | 1008.84 ± 0.56 | 280.65 ± 0.18 | +259.47% | 70.05 ± 0.03 | 64.26 ± 0.05 | +9.00% |
| 512 | 999.73 ± 0.43 | 275.62 ± 0.67 | +262.73% | 66.52 ± 0.03 | 62.84 ± 0.04 | +5.84% |
| 1024 | 961.15 ± 0.34 | 260.93 ± 0.65 | +268.36% | 63.93 ± 0.07 | 60.86 ± 0.05 | +5.05% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
