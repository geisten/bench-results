# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `495156f8079f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1004.00 ± 0.53 | 926.07 ± 2.33 | +8.42% | 147.61 ± 0.13 | 136.89 ± 0.08 | +7.84% |
| 256 | 998.30 ± 0.64 | 909.82 ± 3.31 | +9.73% | 146.38 ± 0.22 | 134.86 ± 0.08 | +8.55% |
| 512 | 984.51 ± 0.47 | 891.50 ± 1.10 | +10.43% | 143.92 ± 0.08 | 133.81 ± 0.07 | +7.55% |
| 1024 | 951.21 ± 0.63 | 870.21 ± 0.86 | +9.31% | 138.49 ± 0.17 | 131.57 ± 0.06 | +5.26% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
