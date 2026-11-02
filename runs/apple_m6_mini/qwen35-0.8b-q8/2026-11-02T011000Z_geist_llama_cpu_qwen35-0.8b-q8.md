# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `e64ff1027649`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 997.68 ± 0.28 | 922.97 ± 0.64 | +8.09% | 144.68 ± 0.14 | 136.95 ± 0.08 | +5.64% |
| 256 | 992.80 ± 0.62 | 909.14 ± 3.36 | +9.20% | 143.42 ± 0.17 | 135.01 ± 0.04 | +6.23% |
| 512 | 979.54 ± 0.55 | 893.38 ± 3.01 | +9.64% | 140.88 ± 0.07 | 133.75 ± 0.05 | +5.32% |
| 1024 | 947.19 ± 0.54 | 868.74 ± 1.71 | +9.03% | 135.99 ± 0.10 | 131.50 ± 0.04 | +3.42% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
