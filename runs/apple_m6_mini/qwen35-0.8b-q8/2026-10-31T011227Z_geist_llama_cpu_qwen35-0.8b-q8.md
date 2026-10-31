# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 994.19 ± 0.74 | 923.82 ± 3.84 | +7.62% | 142.49 ± 0.09 | 134.43 ± 0.43 | +6.00% |
| 256 | 990.06 ± 0.77 | 904.86 ± 3.05 | +9.42% | 141.47 ± 0.11 | 132.77 ± 0.59 | +6.55% |
| 512 | 976.78 ± 0.83 | 862.66 ± 5.04 | +13.23% | 139.23 ± 0.18 | 131.63 ± 0.40 | +5.77% |
| 1024 | 945.72 ± 0.46 | 839.55 ± 2.59 | +12.65% | 134.34 ± 0.07 | 129.37 ± 0.50 | +3.85% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
