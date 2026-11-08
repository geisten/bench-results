# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1000.70 ± 0.99 | 922.70 ± 3.57 | +8.45% | 147.18 ± 0.20 | 134.47 ± 0.16 | +9.45% |
| 256 | 995.11 ± 1.08 | 902.21 ± 7.54 | +10.30% | 145.85 ± 0.12 | 132.49 ± 0.35 | +10.08% |
| 512 | 980.64 ± 0.97 | 890.39 ± 0.98 | +10.14% | 143.26 ± 0.26 | 131.27 ± 0.29 | +9.13% |
| 1024 | 946.76 ± 2.08 | 867.74 ± 2.10 | +9.11% | 137.86 ± 0.31 | 129.29 ± 0.21 | +6.63% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
