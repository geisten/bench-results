# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1688.49 ± 9.02 | 980.88 ± 2.99 | +72.14% | 81.13 ± 0.42 | 70.19 ± 0.39 | +15.60% |
| 256 | 1714.52 ± 15.65 | 1005.59 ± 9.80 | +70.50% | 80.60 ± 0.70 | 70.27 ± 0.57 | +14.70% |
| 512 | 1723.13 ± 11.22 | 1020.69 ± 12.57 | +68.82% | 80.90 ± 0.25 | 69.78 ± 0.69 | +15.93% |
| 1024 | 1713.11 ± 15.69 | 1016.43 ± 17.26 | +68.54% | 80.16 ± 0.55 | 69.76 ± 0.15 | +14.90% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
