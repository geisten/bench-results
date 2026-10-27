# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `df665fe9c736`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1206.27 ± 7.14 | 723.24 ± 3.13 | +66.79% | 77.39 ± 0.57 | 66.65 ± 0.77 | +16.10% |
| 256 | 1187.75 ± 13.09 | 750.35 ± 7.15 | +58.29% | 77.22 ± 0.43 | 68.09 ± 0.79 | +13.41% |
| 512 | 1193.14 ± 4.56 | 760.35 ± 4.46 | +56.92% | 76.81 ± 0.42 | 67.96 ± 1.31 | +13.01% |
| 1024 | 1193.94 ± 5.85 | 757.32 ± 5.60 | +57.65% | 76.58 ± 0.48 | 68.35 ± 0.60 | +12.05% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
