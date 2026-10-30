# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1711.52 ± 25.14 | 993.58 ± 6.45 | +72.26% | 82.32 ± 0.25 | 71.60 ± 0.36 | +14.96% |
| 256 | 1740.81 ± 9.67 | 1026.81 ± 8.24 | +69.54% | 82.03 ± 0.35 | 71.26 ± 0.84 | +15.11% |
| 512 | 1746.07 ± 8.96 | 1041.45 ± 3.02 | +67.66% | 81.67 ± 0.46 | 70.35 ± 0.62 | +16.09% |
| 1024 | 1744.55 ± 5.53 | 1033.19 ± 11.30 | +68.85% | 81.02 ± 0.37 | 70.15 ± 0.80 | +15.49% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
