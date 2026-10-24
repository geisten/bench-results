# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `14ac9f78e1df`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1672.10 ± 10.93 | 983.77 ± 8.87 | +69.97% | 81.75 ± 0.36 | 70.20 ± 0.62 | +16.45% |
| 256 | 1715.15 ± 7.38 | 1021.83 ± 7.85 | +67.85% | 81.56 ± 0.51 | 71.11 ± 0.74 | +14.69% |
| 512 | 1719.52 ± 4.55 | 1029.41 ± 7.41 | +67.04% | 81.70 ± 0.22 | 70.76 ± 0.54 | +15.45% |
| 1024 | 1715.26 ± 9.37 | 1024.87 ± 6.99 | +67.36% | 81.28 ± 0.42 | 70.12 ± 0.57 | +15.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
