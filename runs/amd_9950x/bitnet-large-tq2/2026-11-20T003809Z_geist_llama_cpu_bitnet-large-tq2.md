# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2562.70 ± 29.13 | 1359.72 ± 3.28 | +88.47% | 326.48 ± 1.44 | 241.34 ± 1.38 | +35.28% |
| 256 | 2444.57 ± 41.64 | 1404.88 ± 7.42 | +74.01% | 307.81 ± 1.39 | 214.37 ± 2.17 | +43.59% |
| 512 | 2325.75 ± 12.38 | 1372.32 ± 5.51 | +69.48% | 276.50 ± 1.15 | 184.67 ± 0.68 | +49.73% |
| 1024 | 2076.96 ± 19.71 | 1324.77 ± 1.66 | +56.78% | 220.33 ± 3.32 | 145.40 ± 1.09 | +51.53% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
