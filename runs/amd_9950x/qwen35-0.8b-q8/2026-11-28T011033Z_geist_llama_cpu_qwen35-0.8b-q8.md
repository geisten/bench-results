# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `a7a01a052466`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1684.78 ± 7.04 | 975.58 ± 7.72 | +72.70% | 80.86 ± 0.36 | 69.18 ± 1.08 | +16.89% |
| 256 | 1718.27 ± 6.02 | 1000.57 ± 5.06 | +71.73% | 80.75 ± 0.54 | 68.61 ± 0.79 | +17.70% |
| 512 | 1713.04 ± 9.25 | 1008.18 ± 22.78 | +69.91% | 80.52 ± 0.42 | 68.38 ± 0.97 | +17.75% |
| 1024 | 1710.90 ± 8.38 | 1014.44 ± 6.89 | +68.65% | 80.54 ± 0.29 | 68.66 ± 0.82 | +17.31% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
