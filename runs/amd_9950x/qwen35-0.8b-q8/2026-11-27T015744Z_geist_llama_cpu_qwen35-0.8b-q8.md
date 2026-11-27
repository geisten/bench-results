# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `f4ae43569c6a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1690.31 ± 10.00 | 855.72 ± 122.69 | +97.53% | 81.14 ± 0.69 | 68.81 ± 0.13 | +17.92% |
| 256 | 1719.70 ± 7.62 | 900.72 ± 106.95 | +90.93% | 81.10 ± 0.76 | 68.27 ± 0.96 | +18.80% |
| 512 | 1726.77 ± 11.45 | 976.95 ± 59.41 | +76.75% | 81.25 ± 0.52 | 67.49 ± 0.90 | +20.39% |
| 1024 | 1724.25 ± 10.66 | 1014.59 ± 23.26 | +69.95% | 79.74 ± 1.21 | 66.61 ± 0.47 | +19.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
