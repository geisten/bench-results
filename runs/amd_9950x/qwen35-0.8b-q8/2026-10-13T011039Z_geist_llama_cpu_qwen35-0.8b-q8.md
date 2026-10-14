# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `db8314e2a3a3`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1681.17 ± 23.66 | 976.04 ± 7.26 | +72.24% | 80.70 ± 0.20 | 68.36 ± 0.53 | +18.05% |
| 256 | 1706.14 ± 17.39 | 1021.93 ± 9.97 | +66.95% | 80.81 ± 0.27 | 69.29 ± 0.38 | +16.62% |
| 512 | 1719.03 ± 9.66 | 1032.34 ± 8.38 | +66.52% | 80.64 ± 0.18 | 68.64 ± 0.27 | +17.49% |
| 1024 | 1717.74 ± 3.98 | 1024.68 ± 8.73 | +67.64% | 80.41 ± 0.82 | 68.04 ± 0.41 | +18.17% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
