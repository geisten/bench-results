# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `002ea9d90274`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1672.43 ± 25.10 | 985.41 ± 10.80 | +69.72% | 79.64 ± 0.79 | 67.86 ± 0.66 | +17.36% |
| 256 | 1703.15 ± 23.64 | 1016.66 ± 17.57 | +67.52% | 79.79 ± 0.71 | 68.04 ± 0.61 | +17.26% |
| 512 | 1721.28 ± 7.18 | 992.73 ± 38.86 | +73.39% | 80.48 ± 0.43 | 67.58 ± 0.50 | +19.09% |
| 1024 | 1717.87 ± 9.33 | 1005.89 ± 17.38 | +70.78% | 80.24 ± 0.37 | 67.81 ± 0.77 | +18.32% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
