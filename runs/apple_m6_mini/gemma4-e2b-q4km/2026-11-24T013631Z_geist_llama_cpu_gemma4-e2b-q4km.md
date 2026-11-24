# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 543.67 ± 0.59 | 283.89 ± 0.10 | +91.50% | 72.53 ± 0.07 | 66.86 ± 0.07 | +8.48% |
| 256 | 713.84 ± 0.49 | 280.72 ± 0.26 | +154.29% | 70.48 ± 0.05 | 64.23 ± 0.05 | +9.73% |
| 512 | 822.94 ± 0.49 | 275.32 ± 0.67 | +198.91% | 66.90 ± 0.12 | 62.89 ± 0.03 | +6.38% |
| 1024 | 859.53 ± 0.72 | 260.82 ± 0.35 | +229.55% | 64.19 ± 0.15 | 60.88 ± 0.03 | +5.44% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
