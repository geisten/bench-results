# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `13921becb240`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1717.84 ± 13.80 | 991.49 ± 5.28 | +73.26% | 81.15 ± 0.95 | 69.20 ± 0.11 | +17.26% |
| 256 | 1739.45 ± 6.42 | 1032.76 ± 7.43 | +68.43% | 81.79 ± 0.40 | 69.57 ± 0.80 | +17.56% |
| 512 | 1743.40 ± 4.31 | 1030.62 ± 17.57 | +69.16% | 81.56 ± 0.26 | 68.99 ± 0.99 | +18.23% |
| 1024 | 1744.15 ± 9.47 | 994.20 ± 46.60 | +75.43% | 80.40 ± 0.89 | 68.52 ± 1.02 | +17.34% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
