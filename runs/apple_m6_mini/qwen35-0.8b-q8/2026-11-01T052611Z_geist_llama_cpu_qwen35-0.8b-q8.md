# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 982.88 ± 1.64 | 922.82 ± 5.18 | +6.51% | 140.25 ± 0.14 | 134.35 ± 0.16 | +4.39% |
| 256 | 980.12 ± 0.66 | 905.70 ± 10.71 | +8.22% | 139.34 ± 0.15 | 132.52 ± 0.04 | +5.14% |
| 512 | 966.94 ± 1.18 | 890.88 ± 2.13 | +8.54% | 137.37 ± 0.13 | 131.31 ± 0.14 | +4.61% |
| 1024 | 935.73 ± 0.79 | 868.58 ± 1.10 | +7.73% | 132.63 ± 0.10 | 129.28 ± 0.16 | +2.59% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
