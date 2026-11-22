# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `d46135a24bb6`; llama.cpp `d81235049384`.

Host profile `apple_m6_mini_metal`: 4-thread prefill, 4-thread decode, geist on `metal`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on Apple M6, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: Apple M6 (6 physical cores), Darwin 27.2.0.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 5829.05 ± 50.46 | 5189.98 ± 24.84 | +12.31% | 151.85 ± 0.18 | 148.44 ± 0.25 | +2.30% |
| 256 | 6934.10 ± 12.28 | 6355.27 ± 12.99 | +9.11% | 151.95 ± 0.09 | 145.03 ± 0.31 | +4.77% |
| 512 | 7095.44 ± 21.75 | 6220.54 ± 45.55 | +14.06% | 151.32 ± 0.09 | 144.36 ± 0.45 | +4.82% |
| 1024 | 7095.79 ± 14.06 | 6281.28 ± 35.70 | +12.97% | 150.19 ± 0.09 | 143.31 ± 1.03 | +4.80% |

Every run started on AC power with Low Power Mode off (power gate, pmset); each run's machine state records it.

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
