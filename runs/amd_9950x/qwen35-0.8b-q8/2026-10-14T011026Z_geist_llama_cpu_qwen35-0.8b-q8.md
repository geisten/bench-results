# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-0.8b-q8_0.gguf` (`0ad885ffd4bb022fc4f0d33a3308fa108ef8613159d3b3a67e23abca056b7a6c`)

geist `527bf29dd426`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1682.56 ± 11.92 | 982.30 ± 10.61 | +71.29% | 81.03 ± 0.83 | 68.67 ± 0.48 | +18.00% |
| 256 | 1715.74 ± 12.41 | 1010.88 ± 15.71 | +69.73% | 81.41 ± 0.35 | 69.12 ± 0.35 | +17.78% |
| 512 | 1723.76 ± 11.43 | 1032.93 ± 6.62 | +66.88% | 81.26 ± 0.29 | 68.93 ± 0.54 | +17.88% |
| 1024 | 1726.76 ± 5.00 | 1024.14 ± 9.39 | +68.61% | 81.44 ± 0.29 | 68.01 ± 0.51 | +19.74% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
