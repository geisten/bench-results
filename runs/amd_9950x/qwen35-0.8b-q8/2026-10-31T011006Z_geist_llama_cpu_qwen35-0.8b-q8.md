# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1707.52 ± 8.86 | 993.12 ± 7.38 | +71.94% | 81.66 ± 0.48 | 69.98 ± 0.32 | +16.68% |
| 256 | 1726.12 ± 15.61 | 1033.19 ± 7.47 | +67.07% | 81.44 ± 0.30 | 70.53 ± 0.75 | +15.46% |
| 512 | 1738.35 ± 11.74 | 1014.11 ± 21.00 | +71.42% | 81.06 ± 0.25 | 70.43 ± 0.52 | +15.10% |
| 1024 | 1735.93 ± 7.76 | 1031.80 ± 9.30 | +68.24% | 80.53 ± 0.36 | 69.61 ± 0.17 | +15.68% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
