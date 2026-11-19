# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 986.67 ± 0.51 | 921.59 ± 2.19 | +7.06% | 140.92 ± 0.11 | 134.45 ± 0.40 | +4.81% |
| 256 | 980.49 ± 0.81 | 908.76 ± 3.30 | +7.89% | 139.95 ± 0.19 | 132.51 ± 0.11 | +5.61% |
| 512 | 966.14 ± 0.57 | 876.51 ± 3.39 | +10.23% | 137.64 ± 0.10 | 131.41 ± 0.20 | +4.74% |
| 1024 | 934.02 ± 1.09 | 855.65 ± 6.57 | +9.16% | 133.13 ± 0.07 | 129.58 ± 0.21 | +2.74% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
