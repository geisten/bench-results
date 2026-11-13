# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `0b27a7bb678a`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1702.89 ± 7.41 | 994.38 ± 6.11 | +71.25% | 81.34 ± 0.68 | 69.95 ± 0.34 | +16.28% |
| 256 | 1724.24 ± 7.66 | 1040.90 ± 12.18 | +65.65% | 81.78 ± 0.24 | 71.03 ± 0.28 | +15.13% |
| 512 | 1730.14 ± 19.30 | 1038.25 ± 16.72 | +66.64% | 80.86 ± 0.63 | 70.63 ± 0.47 | +14.48% |
| 1024 | 1729.09 ± 9.60 | 1045.70 ± 8.92 | +65.35% | 80.70 ± 0.65 | 69.93 ± 0.86 | +15.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
