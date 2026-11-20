# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1668.69 ± 39.97 | 986.66 ± 4.15 | +69.13% | 81.09 ± 0.38 | 69.89 ± 0.49 | +16.02% |
| 256 | 1718.17 ± 15.67 | 1006.16 ± 13.84 | +70.76% | 81.05 ± 0.32 | 70.34 ± 0.33 | +15.21% |
| 512 | 1729.10 ± 16.84 | 995.14 ± 53.69 | +73.75% | 80.95 ± 0.20 | 70.24 ± 0.49 | +15.26% |
| 1024 | 1728.67 ± 8.96 | 1025.35 ± 24.58 | +68.59% | 80.70 ± 0.29 | 69.54 ± 0.94 | +16.05% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
