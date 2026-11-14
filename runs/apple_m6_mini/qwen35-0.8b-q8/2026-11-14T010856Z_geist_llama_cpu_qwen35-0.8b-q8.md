# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini`: 6-thread prefill, 5-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 981.62 ± 3.62 | 921.50 ± 3.39 | +6.52% | 138.88 ± 0.27 | 134.17 ± 0.31 | +3.51% |
| 256 | 975.06 ± 3.61 | 906.39 ± 6.58 | +7.58% | 137.69 ± 0.36 | 132.22 ± 0.22 | +4.14% |
| 512 | 964.62 ± 3.19 | 892.59 ± 2.74 | +8.07% | 135.99 ± 0.32 | 131.17 ± 0.27 | +3.68% |
| 1024 | 928.99 ± 4.08 | 864.44 ± 4.53 | +7.47% | 131.61 ± 0.30 | 129.12 ± 0.21 | +1.92% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
