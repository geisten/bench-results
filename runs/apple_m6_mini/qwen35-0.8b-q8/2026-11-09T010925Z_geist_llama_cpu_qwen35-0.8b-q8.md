# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a4d332c604a2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 990.00 ± 0.95 | 924.76 ± 2.85 | +7.05% | 142.79 ± 0.21 | 134.14 ± 0.55 | +6.45% |
| 256 | 985.87 ± 1.01 | 902.12 ± 6.86 | +9.28% | 141.73 ± 0.12 | 131.92 ± 0.61 | +7.44% |
| 512 | 968.57 ± 2.91 | 873.55 ± 13.76 | +10.88% | 139.53 ± 0.09 | 130.80 ± 0.61 | +6.67% |
| 1024 | 938.33 ± 1.64 | 842.28 ± 7.69 | +11.40% | 134.83 ± 0.09 | 129.26 ± 0.65 | +4.31% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
