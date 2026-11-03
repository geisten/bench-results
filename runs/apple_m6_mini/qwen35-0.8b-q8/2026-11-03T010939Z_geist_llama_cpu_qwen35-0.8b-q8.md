# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1001.23 ± 0.87 | 925.70 ± 1.82 | +8.16% | 145.63 ± 0.11 | 134.94 ± 0.29 | +7.92% |
| 256 | 997.70 ± 0.62 | 902.47 ± 1.74 | +10.55% | 144.44 ± 0.20 | 132.88 ± 0.10 | +8.70% |
| 512 | 983.04 ± 0.89 | 883.10 ± 6.57 | +11.32% | 142.10 ± 0.23 | 131.82 ± 0.16 | +7.80% |
| 1024 | 949.34 ± 0.69 | 861.35 ± 4.23 | +10.22% | 137.12 ± 0.24 | 129.67 ± 0.15 | +5.75% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
