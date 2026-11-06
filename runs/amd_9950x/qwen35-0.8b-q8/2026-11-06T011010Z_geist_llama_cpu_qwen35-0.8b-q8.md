# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1695.41 ± 17.82 | 991.13 ± 9.32 | +71.06% | 81.56 ± 0.66 | 69.11 ± 0.92 | +18.01% |
| 256 | 1727.50 ± 16.38 | 1027.12 ± 8.71 | +68.19% | 81.48 ± 0.47 | 68.57 ± 0.43 | +18.83% |
| 512 | 1745.62 ± 8.33 | 1038.07 ± 5.22 | +68.16% | 81.38 ± 0.44 | 68.16 ± 0.50 | +19.40% |
| 1024 | 1743.83 ± 6.18 | 1029.33 ± 11.28 | +69.41% | 80.43 ± 0.53 | 68.08 ± 0.39 | +18.14% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
