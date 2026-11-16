# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1686.23 ± 19.87 | 982.91 ± 12.06 | +71.55% | 81.75 ± 0.36 | 70.84 ± 0.22 | +15.40% |
| 256 | 1729.28 ± 11.25 | 1018.58 ± 11.80 | +69.77% | 82.65 ± 0.09 | 71.09 ± 0.59 | +16.25% |
| 512 | 1737.38 ± 7.67 | 983.84 ± 26.68 | +76.59% | 82.42 ± 0.04 | 70.33 ± 0.39 | +17.19% |
| 1024 | 1737.09 ± 8.29 | 1013.76 ± 18.04 | +71.35% | 81.77 ± 0.21 | 69.81 ± 0.55 | +17.14% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
