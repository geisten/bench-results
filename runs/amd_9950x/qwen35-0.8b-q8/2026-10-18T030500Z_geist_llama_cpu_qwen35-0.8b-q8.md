# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1683.96 ± 4.54 | 991.53 ± 11.46 | +69.83% | 81.48 ± 0.39 | 70.87 ± 0.71 | +14.97% |
| 256 | 1722.38 ± 12.56 | 1039.20 ± 9.94 | +65.74% | 81.38 ± 0.17 | 71.25 ± 0.60 | +14.22% |
| 512 | 1727.91 ± 11.92 | 1039.53 ± 6.07 | +66.22% | 81.35 ± 0.55 | 70.73 ± 0.71 | +15.01% |
| 1024 | 1731.07 ± 9.50 | 1029.50 ± 13.66 | +68.15% | 81.08 ± 0.59 | 70.18 ± 0.68 | +15.52% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
