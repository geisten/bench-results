# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `9287d0c3734e`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 6005.44 ± 18.94 | 5273.53 ± 7.45 | +13.88% | 155.59 ± 0.13 | 150.89 ± 0.18 | +3.11% |
| 256 | 7040.32 ± 21.10 | 6448.49 ± 8.86 | +9.18% | 155.42 ± 0.03 | 147.38 ± 0.16 | +5.46% |
| 512 | 7200.57 ± 8.76 | 6253.70 ± 70.72 | +15.14% | 154.84 ± 0.05 | 147.22 ± 0.34 | +5.17% |
| 1024 | 7186.95 ± 5.43 | 6327.66 ± 82.77 | +13.58% | 153.76 ± 0.11 | 143.07 ± 1.32 | +7.47% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
