# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `d231cb8104bc`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1645.00 ± 65.20 | 913.48 ± 62.57 | +80.08% | 79.47 ± 2.58 | 68.89 ± 0.78 | +15.36% |
| 256 | 1180.60 ± 25.09 | 888.08 ± 124.03 | +32.94% | 76.31 ± 1.41 | 69.08 ± 0.62 | +10.46% |
| 512 | 1347.20 ± 238.97 | 1021.24 ± 12.88 | +31.92% | 78.48 ± 1.77 | 69.80 ± 0.80 | +12.43% |
| 1024 | 1721.19 ± 12.09 | 1017.06 ± 16.00 | +69.23% | 79.53 ± 0.56 | 68.72 ± 0.86 | +15.74% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
