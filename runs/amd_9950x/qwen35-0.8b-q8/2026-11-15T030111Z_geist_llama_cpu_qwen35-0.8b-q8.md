# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1699.24 ± 23.20 | 992.11 ± 6.09 | +71.28% | 81.64 ± 1.02 | 70.43 ± 0.57 | +15.92% |
| 256 | 1723.90 ± 4.70 | 1027.64 ± 3.35 | +67.75% | 81.94 ± 0.51 | 70.38 ± 0.39 | +16.43% |
| 512 | 1746.76 ± 8.27 | 1034.19 ± 13.78 | +68.90% | 81.87 ± 0.43 | 69.52 ± 0.90 | +17.76% |
| 1024 | 1742.74 ± 5.37 | 1010.58 ± 24.08 | +72.45% | 81.42 ± 0.52 | 69.49 ± 0.45 | +17.17% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
