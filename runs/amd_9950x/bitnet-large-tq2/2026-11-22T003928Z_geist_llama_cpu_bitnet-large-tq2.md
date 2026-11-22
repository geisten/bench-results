# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2588.84 ± 37.85 | 1353.95 ± 5.97 | +91.21% | 326.40 ± 2.61 | 248.55 ± 0.96 | +31.32% |
| 256 | 2492.35 ± 26.57 | 1382.95 ± 8.96 | +80.22% | 308.69 ± 0.75 | 218.62 ± 0.88 | +41.20% |
| 512 | 2316.35 ± 34.54 | 1370.58 ± 2.05 | +69.01% | 274.88 ± 1.09 | 190.01 ± 0.81 | +44.66% |
| 1024 | 2070.44 ± 13.99 | 1323.86 ± 2.50 | +56.39% | 219.31 ± 3.64 | 147.32 ± 1.45 | +48.87% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
