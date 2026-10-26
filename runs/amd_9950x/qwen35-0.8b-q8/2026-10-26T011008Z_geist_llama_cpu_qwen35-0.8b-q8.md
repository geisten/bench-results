# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `eedaae6cae7b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1691.55 ± 21.23 | 993.71 ± 5.80 | +70.23% | 82.24 ± 0.13 | 71.42 ± 0.20 | +15.16% |
| 256 | 1732.91 ± 4.27 | 1040.71 ± 4.20 | +66.51% | 81.96 ± 0.40 | 71.23 ± 0.54 | +15.06% |
| 512 | 1735.70 ± 10.11 | 1006.74 ± 39.50 | +72.41% | 81.71 ± 0.44 | 69.91 ± 0.45 | +16.88% |
| 1024 | 1730.08 ± 7.85 | 1033.70 ± 9.72 | +67.37% | 81.25 ± 0.34 | 69.37 ± 0.53 | +17.13% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
