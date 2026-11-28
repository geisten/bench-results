# Current CPU head-to-head: geist vs llama.cpp

Model: `gemma4-e2b-Q4_K_M.gguf` (`740185b21d22ceb83a11c3aa62ad5842ef32c70f6096d756bbee85a1e4ec34b8`)

geist `a7a01a052466`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 939.08 ± 0.32 | 283.67 ± 0.13 | +231.05% | 72.57 ± 0.03 | 66.42 ± 0.04 | +9.25% |
| 256 | 1006.86 ± 0.59 | 280.35 ± 0.25 | +259.15% | 70.39 ± 0.02 | 63.87 ± 0.03 | +10.21% |
| 512 | 998.28 ± 0.42 | 275.51 ± 0.53 | +262.33% | 66.75 ± 0.02 | 62.50 ± 0.08 | +6.79% |
| 1024 | 957.50 ± 0.37 | 260.72 ± 0.45 | +267.25% | 64.12 ± 0.09 | 60.44 ± 0.10 | +6.08% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
