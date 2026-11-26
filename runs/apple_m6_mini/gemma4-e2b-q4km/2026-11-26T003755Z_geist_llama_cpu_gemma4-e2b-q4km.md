# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 940.72 ± 0.52 | 283.99 ± 0.09 | +231.25% | 72.84 ± 0.04 | 66.86 ± 0.03 | +8.95% |
| 256 | 1008.38 ± 0.34 | 280.66 ± 0.09 | +259.29% | 70.70 ± 0.02 | 64.25 ± 0.01 | +10.04% |
| 512 | 999.59 ± 0.76 | 276.29 ± 0.24 | +261.79% | 67.06 ± 0.05 | 62.83 ± 0.02 | +6.74% |
| 1024 | 960.68 ± 0.48 | 261.84 ± 0.55 | +266.90% | 64.50 ± 0.05 | 60.80 ± 0.04 | +6.09% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
