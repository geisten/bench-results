# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a1751c84f0d4`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1689.33 ± 13.38 | 973.36 ± 10.68 | +73.56% | 80.77 ± 1.18 | 68.78 ± 0.24 | +17.43% |
| 256 | 1236.99 ± 80.72 | 985.99 ± 30.60 | +25.46% | 78.56 ± 1.85 | 69.38 ± 1.94 | +13.24% |
| 512 | 1693.72 ± 27.45 | 1008.54 ± 25.84 | +67.94% | 79.34 ± 1.66 | 68.63 ± 1.25 | +15.61% |
| 1024 | 1707.13 ± 12.25 | 1003.69 ± 22.71 | +70.08% | 79.20 ± 1.34 | 68.16 ± 0.46 | +16.19% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
