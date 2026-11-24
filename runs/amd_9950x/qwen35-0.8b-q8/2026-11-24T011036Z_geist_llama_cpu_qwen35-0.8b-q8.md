# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1678.09 ± 40.31 | 990.25 ± 7.42 | +69.46% | 80.60 ± 1.02 | 68.52 ± 0.22 | +17.63% |
| 256 | 1720.03 ± 11.19 | 1022.22 ± 12.33 | +68.27% | 80.76 ± 0.32 | 68.19 ± 0.66 | +18.44% |
| 512 | 1725.48 ± 9.81 | 1020.59 ± 26.26 | +69.07% | 80.69 ± 0.32 | 67.49 ± 0.97 | +19.56% |
| 1024 | 1723.77 ± 12.14 | 1013.72 ± 15.75 | +70.04% | 80.26 ± 0.15 | 67.72 ± 0.50 | +18.51% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
