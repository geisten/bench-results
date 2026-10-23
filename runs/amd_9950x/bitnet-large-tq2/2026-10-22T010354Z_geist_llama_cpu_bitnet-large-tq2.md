# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `f19377734f16`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2525.75 ± 55.36 | 1360.26 ± 3.59 | +85.68% | 324.62 ± 4.27 | 238.87 ± 1.68 | +35.89% |
| 256 | 2504.87 ± 44.89 | 1408.00 ± 7.91 | +77.90% | 307.94 ± 2.47 | 213.66 ± 1.46 | +44.12% |
| 512 | 2331.19 ± 34.75 | 1379.51 ± 4.11 | +68.99% | 275.93 ± 0.72 | 182.44 ± 1.34 | +51.25% |
| 1024 | 2081.14 ± 16.12 | 1327.22 ± 2.50 | +56.80% | 222.51 ± 2.12 | 143.07 ± 1.67 | +55.52% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
