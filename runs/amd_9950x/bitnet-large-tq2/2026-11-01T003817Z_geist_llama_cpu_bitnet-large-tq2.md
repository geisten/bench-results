# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2551.24 ± 67.90 | 1366.03 ± 2.96 | +86.76% | 323.08 ± 1.48 | 244.51 ± 4.59 | +32.13% |
| 256 | 2574.15 ± 35.96 | 1428.68 ± 5.66 | +80.18% | 305.80 ± 1.16 | 212.82 ± 2.13 | +43.69% |
| 512 | 2388.00 ± 18.50 | 1404.61 ± 7.00 | +70.01% | 271.30 ± 3.26 | 184.08 ± 3.49 | +47.38% |
| 1024 | 2146.54 ± 24.44 | 1336.70 ± 1.76 | +60.59% | 214.01 ± 2.71 | 142.96 ± 0.93 | +49.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
