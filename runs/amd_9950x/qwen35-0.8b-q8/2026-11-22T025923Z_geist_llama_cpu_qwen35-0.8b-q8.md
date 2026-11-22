# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1679.39 ± 12.47 | 984.20 ± 7.17 | +70.64% | 81.97 ± 0.42 | 70.39 ± 0.35 | +16.45% |
| 256 | 1708.37 ± 10.25 | 1012.51 ± 5.41 | +68.73% | 81.81 ± 0.24 | 70.68 ± 0.33 | +15.74% |
| 512 | 1722.26 ± 12.21 | 982.79 ± 32.28 | +75.24% | 81.90 ± 0.27 | 70.83 ± 0.29 | +15.64% |
| 1024 | 1716.18 ± 5.10 | 1012.04 ± 6.64 | +69.58% | 81.56 ± 0.10 | 69.14 ± 0.16 | +17.95% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
