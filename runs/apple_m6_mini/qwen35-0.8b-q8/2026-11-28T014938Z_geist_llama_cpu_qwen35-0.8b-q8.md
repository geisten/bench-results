# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b0ee998e552`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1002.79 ± 0.83 | 927.60 ± 2.92 | +8.11% | 146.46 ± 0.20 | 135.40 ± 0.59 | +8.17% |
| 256 | 998.01 ± 1.34 | 907.25 ± 3.63 | +10.00% | 144.90 ± 0.14 | 133.38 ± 0.61 | +8.64% |
| 512 | 982.55 ± 0.79 | 888.66 ± 3.62 | +10.57% | 142.49 ± 0.16 | 132.42 ± 0.41 | +7.61% |
| 1024 | 948.83 ± 1.51 | 864.23 ± 2.19 | +9.79% | 137.25 ± 0.26 | 130.34 ± 0.33 | +5.30% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
