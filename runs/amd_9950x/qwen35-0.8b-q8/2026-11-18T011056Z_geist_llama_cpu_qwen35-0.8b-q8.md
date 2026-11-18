# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1684.14 ± 12.19 | 983.36 ± 2.92 | +71.26% | 80.91 ± 0.54 | 69.63 ± 0.54 | +16.19% |
| 256 | 1710.38 ± 14.53 | 1007.77 ± 10.12 | +69.72% | 80.75 ± 0.83 | 69.08 ± 1.35 | +16.89% |
| 512 | 1730.86 ± 9.60 | 1028.73 ± 10.31 | +68.25% | 80.80 ± 0.77 | 68.85 ± 0.45 | +17.36% |
| 1024 | 1714.78 ± 14.88 | 1019.29 ± 10.38 | +68.23% | 80.36 ± 0.84 | 67.89 ± 0.31 | +18.37% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
