# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 999.56 ± 4.05 | 923.48 ± 3.51 | +8.24% | 146.61 ± 0.18 | 135.95 ± 0.04 | +7.84% |
| 256 | 995.68 ± 0.88 | 912.15 ± 5.31 | +9.16% | 145.64 ± 0.11 | 133.96 ± 0.10 | +8.72% |
| 512 | 980.83 ± 1.09 | 889.99 ± 1.56 | +10.21% | 142.57 ± 0.18 | 132.86 ± 0.06 | +7.31% |
| 1024 | 948.93 ± 0.51 | 864.81 ± 1.05 | +9.73% | 137.43 ± 0.18 | 130.63 ± 0.08 | +5.20% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
