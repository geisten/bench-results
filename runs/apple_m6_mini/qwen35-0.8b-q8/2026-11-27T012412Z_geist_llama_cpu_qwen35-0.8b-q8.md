# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1001.49 ± 1.11 | 922.72 ± 3.48 | +8.54% | 147.25 ± 0.14 | 135.83 ± 0.16 | +8.41% |
| 256 | 996.67 ± 0.43 | 908.77 ± 5.27 | +9.67% | 146.14 ± 0.12 | 133.74 ± 0.17 | +9.27% |
| 512 | 981.50 ± 0.93 | 891.54 ± 3.80 | +10.09% | 143.57 ± 0.19 | 132.65 ± 0.11 | +8.24% |
| 1024 | 948.76 ± 0.84 | 865.77 ± 1.79 | +9.58% | 138.35 ± 0.20 | 130.48 ± 0.05 | +6.02% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
