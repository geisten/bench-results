# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `apple_m1max`: 8-thread prefill, 7-thread decode, geist on `cpu_neon`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M1 Max (8 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1081.59 ± 0.96 | 956.15 ± 0.92 | +13.12% | 112.10 ± 0.36 | 97.43 ± 0.45 | +15.06% |
| 256 | 1075.36 ± 1.02 | 970.71 ± 4.78 | +10.78% | 110.21 ± 0.17 | 97.47 ± 0.28 | +13.07% |
| 512 | 1057.85 ± 1.09 | 957.16 ± 3.51 | +10.52% | 106.50 ± 0.15 | 97.04 ± 0.18 | +9.74% |
| 1024 | 1020.92 ± 1.20 | 942.70 ± 4.36 | +8.30% | 98.47 ± 1.27 | 95.18 ± 0.41 | +3.45% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
