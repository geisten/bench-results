# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 975.93 ± 2.98 | 923.44 ± 3.69 | +5.69% | 135.94 ± 0.49 | 135.97 ± 0.45 | -0.03% |
| 256 | 969.40 ± 2.45 | 905.08 ± 5.84 | +7.11% | 135.15 ± 0.50 | 133.70 ± 0.57 | +1.08% |
| 512 | 954.24 ± 3.98 | 892.00 ± 0.73 | +6.98% | 133.27 ± 0.25 | 132.52 ± 0.49 | +0.57% |
| 1024 | 924.92 ± 2.61 | 871.30 ± 1.23 | +6.15% | 129.18 ± 0.31 | 130.29 ± 0.58 | -0.85% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
