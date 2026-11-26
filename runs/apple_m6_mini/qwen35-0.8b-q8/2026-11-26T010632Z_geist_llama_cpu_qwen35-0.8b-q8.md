# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1003.04 ± 1.08 | 925.69 ± 0.92 | +8.36% | 147.72 ± 0.19 | 135.72 ± 0.16 | +8.85% |
| 256 | 998.51 ± 0.67 | 906.17 ± 6.34 | +10.19% | 146.46 ± 0.28 | 133.70 ± 0.20 | +9.54% |
| 512 | 982.75 ± 0.53 | 886.33 ± 4.51 | +10.88% | 143.84 ± 0.17 | 132.47 ± 0.15 | +8.58% |
| 1024 | 950.00 ± 0.98 | 860.81 ± 5.98 | +10.36% | 138.51 ± 0.21 | 130.27 ± 0.15 | +6.32% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
