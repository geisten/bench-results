# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `64c3d9c4227e`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1696.85 ± 19.05 | 1010.28 ± 10.16 | +67.96% | 82.27 ± 0.13 | 70.39 ± 0.73 | +16.88% |
| 256 | 1735.38 ± 1.92 | 1037.41 ± 9.76 | +67.28% | 82.24 ± 0.18 | 70.01 ± 0.58 | +17.47% |
| 512 | 1749.40 ± 5.22 | 1036.28 ± 22.20 | +68.82% | 82.05 ± 0.23 | 70.25 ± 0.47 | +16.80% |
| 1024 | 1737.17 ± 7.97 | 1042.40 ± 9.10 | +66.65% | 81.57 ± 0.30 | 69.89 ± 0.51 | +16.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
