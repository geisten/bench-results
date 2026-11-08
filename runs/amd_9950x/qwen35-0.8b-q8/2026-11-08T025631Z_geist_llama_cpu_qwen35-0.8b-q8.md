# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1697.49 ± 14.78 | 992.04 ± 7.04 | +71.11% | 81.37 ± 0.33 | 68.98 ± 0.28 | +17.98% |
| 256 | 1722.53 ± 10.90 | 1028.39 ± 5.77 | +67.50% | 80.55 ± 0.93 | 68.54 ± 0.51 | +17.53% |
| 512 | 1743.37 ± 5.59 | 1041.76 ± 18.23 | +67.35% | 79.93 ± 0.72 | 69.25 ± 1.08 | +15.43% |
| 1024 | 1737.15 ± 10.20 | 1019.59 ± 21.12 | +70.38% | 79.47 ± 0.50 | 68.20 ± 0.23 | +16.53% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
