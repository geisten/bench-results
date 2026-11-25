# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1002.60 ± 0.68 | 925.10 ± 4.80 | +8.38% | 147.70 ± 0.36 | 136.91 ± 0.06 | +7.88% |
| 256 | 997.49 ± 1.08 | 910.78 ± 8.14 | +9.52% | 146.33 ± 0.17 | 134.94 ± 0.10 | +8.44% |
| 512 | 982.57 ± 0.65 | 891.98 ± 3.03 | +10.16% | 143.89 ± 0.08 | 133.76 ± 0.10 | +7.57% |
| 1024 | 949.78 ± 1.14 | 868.30 ± 2.28 | +9.38% | 138.74 ± 0.16 | 131.53 ± 0.05 | +5.48% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
