# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `44479afd263d`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1184.39 ± 25.37 | 725.49 ± 9.16 | +63.25% | 79.81 ± 0.07 | 67.67 ± 1.00 | +17.94% |
| 256 | 1182.44 ± 9.24 | 761.15 ± 10.12 | +55.35% | 79.62 ± 0.20 | 67.40 ± 0.54 | +18.13% |
| 512 | 1178.84 ± 7.54 | 773.24 ± 4.65 | +52.45% | 79.55 ± 0.30 | 67.15 ± 1.02 | +18.47% |
| 1024 | 1177.08 ± 6.22 | 768.16 ± 5.51 | +53.23% | 79.42 ± 0.15 | 67.43 ± 1.12 | +17.77% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
