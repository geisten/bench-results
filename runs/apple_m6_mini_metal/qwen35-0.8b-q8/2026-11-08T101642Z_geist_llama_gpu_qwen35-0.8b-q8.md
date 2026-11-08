# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (2 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 6003.33 ± 19.35 | 5271.97 ± 17.59 | +13.87% | 154.52 ± 0.14 | 150.29 ± 0.26 | +2.82% |
| 256 | 7049.72 ± 22.52 | 6466.03 ± 14.30 | +9.03% | 154.31 ± 0.06 | 146.94 ± 0.35 | +5.02% |
| 512 | 7197.78 ± 4.75 | 6280.89 ± 30.23 | +14.60% | 153.72 ± 0.07 | 146.54 ± 0.12 | +4.90% |
| 1024 | 7185.41 ± 5.67 | 6280.02 ± 101.47 | +14.42% | 152.60 ± 0.04 | 145.33 ± 0.89 | +5.00% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
