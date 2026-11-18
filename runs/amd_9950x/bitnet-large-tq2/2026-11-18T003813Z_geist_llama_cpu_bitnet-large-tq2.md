# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `372846765fa0`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2547.31 ± 53.84 | 1362.64 ± 4.24 | +86.94% | 327.50 ± 1.80 | 243.08 ± 1.76 | +34.73% |
| 256 | 2535.46 ± 24.19 | 1396.24 ± 11.33 | +81.59% | 308.27 ± 2.36 | 211.99 ± 1.60 | +45.41% |
| 512 | 2344.09 ± 16.80 | 1375.84 ± 4.68 | +70.38% | 276.36 ± 2.59 | 183.96 ± 1.70 | +50.23% |
| 1024 | 2093.21 ± 10.95 | 1328.06 ± 3.47 | +57.61% | 221.74 ± 3.88 | 145.26 ± 1.05 | +52.66% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
