# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `48a84627b0c5`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1712.34 ± 12.69 | 998.85 ± 11.93 | +71.43% | 81.97 ± 0.36 | 70.51 ± 0.43 | +16.25% |
| 256 | 1725.96 ± 13.21 | 1034.43 ± 12.40 | +66.85% | 81.62 ± 0.23 | 69.80 ± 0.86 | +16.93% |
| 512 | 1734.87 ± 11.84 | 1048.85 ± 9.28 | +65.41% | 81.85 ± 0.60 | 69.18 ± 0.53 | +18.31% |
| 1024 | 1730.84 ± 7.98 | 1034.93 ± 11.59 | +67.24% | 81.64 ± 0.27 | 69.71 ± 0.65 | +17.10% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
