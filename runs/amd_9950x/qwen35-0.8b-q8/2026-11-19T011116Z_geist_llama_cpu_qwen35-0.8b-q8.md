# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f261cadcf982`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1674.11 ± 9.92 | 986.24 ± 4.71 | +69.75% | 81.07 ± 0.33 | 68.82 ± 0.25 | +17.80% |
| 256 | 1720.76 ± 11.16 | 1013.57 ± 13.39 | +69.77% | 81.31 ± 0.29 | 69.12 ± 0.32 | +17.64% |
| 512 | 1721.79 ± 10.06 | 1018.76 ± 23.91 | +69.01% | 81.22 ± 0.36 | 68.78 ± 0.18 | +18.09% |
| 1024 | 1721.16 ± 2.49 | 1023.12 ± 14.72 | +68.23% | 80.79 ± 0.26 | 68.75 ± 0.80 | +17.50% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
