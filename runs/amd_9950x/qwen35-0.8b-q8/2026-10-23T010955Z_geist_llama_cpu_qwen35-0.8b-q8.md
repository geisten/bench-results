# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `cdc4ba43c58a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1696.18 ± 9.73 | 976.33 ± 8.69 | +73.73% | 81.08 ± 1.22 | 69.74 ± 0.49 | +16.27% |
| 256 | 1717.92 ± 11.27 | 1000.40 ± 5.72 | +71.72% | 80.51 ± 0.43 | 69.92 ± 1.26 | +15.14% |
| 512 | 1730.12 ± 9.64 | 1035.76 ± 8.25 | +67.04% | 80.03 ± 0.35 | 69.46 ± 0.80 | +15.23% |
| 1024 | 1705.25 ± 11.75 | 1029.44 ± 13.63 | +65.65% | 79.97 ± 1.00 | 69.08 ± 0.84 | +15.77% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
