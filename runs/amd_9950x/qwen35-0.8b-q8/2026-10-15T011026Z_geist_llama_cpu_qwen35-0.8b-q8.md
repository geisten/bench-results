# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ebcdfb017ba6`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1665.24 ± 18.32 | 973.52 ± 4.16 | +71.05% | 79.93 ± 0.84 | 68.35 ± 0.47 | +16.95% |
| 256 | 1695.08 ± 21.28 | 1011.88 ± 6.98 | +67.52% | 80.83 ± 0.49 | 69.27 ± 0.67 | +16.70% |
| 512 | 1720.15 ± 24.65 | 1024.16 ± 5.42 | +67.96% | 80.42 ± 0.65 | 68.80 ± 0.52 | +16.89% |
| 1024 | 1714.36 ± 16.90 | 1017.58 ± 8.15 | +68.47% | 80.22 ± 0.51 | 68.39 ± 0.43 | +17.29% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
