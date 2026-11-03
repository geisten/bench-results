# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `57f58a18c43f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1190.33 ± 11.84 | 726.78 ± 5.50 | +63.78% | 78.49 ± 1.67 | 67.43 ± 2.05 | +16.41% |
| 256 | 1188.56 ± 5.74 | 754.37 ± 10.25 | +57.56% | 80.26 ± 0.36 | 65.96 ± 1.34 | +21.68% |
| 512 | 1187.95 ± 7.23 | 757.92 ± 7.31 | +56.74% | 80.04 ± 0.26 | 66.07 ± 0.43 | +21.14% |
| 1024 | 1188.69 ± 6.34 | 759.04 ± 7.07 | +56.60% | 79.69 ± 0.16 | 66.42 ± 0.62 | +19.98% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
