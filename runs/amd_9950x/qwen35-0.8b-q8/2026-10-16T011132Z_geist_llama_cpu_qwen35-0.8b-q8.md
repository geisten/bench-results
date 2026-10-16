# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `fda9c7a98c7b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1674.59 ± 15.31 | 980.99 ± 9.39 | +70.70% | 81.04 ± 0.40 | 67.92 ± 0.55 | +19.32% |
| 256 | 1719.05 ± 4.67 | 1010.06 ± 6.35 | +70.19% | 81.54 ± 0.41 | 69.47 ± 0.27 | +17.37% |
| 512 | 1721.01 ± 2.91 | 1011.79 ± 19.76 | +70.10% | 81.07 ± 0.26 | 68.11 ± 0.74 | +19.04% |
| 1024 | 1715.13 ± 8.84 | 1024.44 ± 16.16 | +67.42% | 80.81 ± 0.36 | 67.64 ± 0.39 | +19.46% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
