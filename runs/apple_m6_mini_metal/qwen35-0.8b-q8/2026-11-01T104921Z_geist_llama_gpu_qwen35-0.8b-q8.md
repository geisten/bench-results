# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.0.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5986.34 ± 14.03 | 5276.64 ± 10.82 | +13.45% | 154.23 ± 0.06 | 156.92 ± 0.16 | -1.72% |
| 256 | 7034.90 ± 9.18 | 6435.79 ± 24.98 | +9.31% | 154.10 ± 0.04 | 151.50 ± 0.16 | +1.71% |
| 512 | 7181.78 ± 4.23 | 6308.49 ± 34.19 | +13.84% | 153.45 ± 0.08 | 151.35 ± 0.20 | +1.39% |
| 1024 | 7172.30 ± 2.91 | 6341.73 ± 18.07 | +13.10% | 152.37 ± 0.07 | 147.01 ± 1.07 | +3.65% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
