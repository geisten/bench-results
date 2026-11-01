# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1699.33 ± 15.67 | 990.82 ± 11.47 | +71.51% | 81.76 ± 0.39 | 70.91 ± 0.43 | +15.30% |
| 256 | 1716.92 ± 18.88 | 1032.66 ± 11.53 | +66.26% | 81.96 ± 0.19 | 70.70 ± 0.69 | +15.92% |
| 512 | 1742.79 ± 11.29 | 1033.34 ± 8.22 | +68.65% | 82.08 ± 0.33 | 69.99 ± 0.84 | +17.27% |
| 1024 | 1740.29 ± 4.85 | 1043.23 ± 8.11 | +66.82% | 81.60 ± 0.47 | 69.79 ± 0.59 | +16.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
