# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `c212773b0268`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1694.49 ± 12.39 | 985.67 ± 6.20 | +71.91% | 81.75 ± 0.29 | 68.46 ± 0.34 | +19.42% |
| 256 | 1732.39 ± 12.41 | 1031.87 ± 5.15 | +67.89% | 81.66 ± 0.17 | 68.35 ± 0.56 | +19.48% |
| 512 | 1736.87 ± 5.20 | 1038.23 ± 9.12 | +67.29% | 81.26 ± 0.28 | 68.00 ± 0.41 | +19.49% |
| 1024 | 1738.64 ± 5.77 | 1023.88 ± 25.28 | +69.81% | 81.16 ± 0.13 | 67.77 ± 0.74 | +19.77% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
