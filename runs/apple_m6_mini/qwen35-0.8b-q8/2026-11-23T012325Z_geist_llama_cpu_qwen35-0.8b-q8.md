# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a1751c84f0d4`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1002.44 ± 0.74 | 921.45 ± 3.62 | +8.79% | 143.75 ± 0.29 | 132.59 ± 0.20 | +8.42% |
| 256 | 994.70 ± 1.29 | 903.43 ± 2.88 | +10.10% | 142.29 ± 0.32 | 130.60 ± 0.15 | +8.95% |
| 512 | 980.91 ± 1.59 | 877.43 ± 5.19 | +11.79% | 139.91 ± 0.27 | 129.63 ± 0.25 | +7.93% |
| 1024 | 945.97 ± 1.79 | 846.96 ± 6.06 | +11.69% | 134.61 ± 0.36 | 127.29 ± 0.20 | +5.75% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
