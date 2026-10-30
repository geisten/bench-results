# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `50863de30fe7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2585.81 ± 36.64 | 1363.69 ± 7.75 | +89.62% | 325.93 ± 2.57 | 240.15 ± 5.86 | +35.72% |
| 256 | 2585.67 ± 37.99 | 1425.97 ± 3.00 | +81.33% | 307.71 ± 2.24 | 216.97 ± 1.32 | +41.82% |
| 512 | 2379.18 ± 16.83 | 1403.82 ± 5.03 | +69.48% | 274.34 ± 1.58 | 185.49 ± 1.63 | +47.90% |
| 1024 | 2132.41 ± 9.70 | 1336.73 ± 1.83 | +59.52% | 221.67 ± 2.71 | 147.08 ± 1.01 | +50.71% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
