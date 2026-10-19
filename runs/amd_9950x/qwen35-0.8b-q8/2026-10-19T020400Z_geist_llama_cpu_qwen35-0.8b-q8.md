# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `2b5263f87833`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1191.06 ± 31.44 | 749.63 ± 21.32 | +58.89% | 78.55 ± 0.70 | 68.76 ± 0.57 | +14.23% |
| 256 | 1196.96 ± 14.14 | 769.64 ± 20.80 | +55.52% | 79.26 ± 1.05 | 68.23 ± 2.08 | +16.18% |
| 512 | 1198.89 ± 11.44 | 783.42 ± 14.12 | +53.03% | 79.02 ± 1.20 | 68.35 ± 1.27 | +15.60% |
| 1024 | 1188.70 ± 9.44 | 773.41 ± 35.98 | +53.69% | 79.55 ± 0.42 | 67.88 ± 0.86 | +17.20% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
