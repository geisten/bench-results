# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `db8314e2a3a3`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2366.48 ± 36.56 | 1360.05 ± 5.10 | +74.00% | 319.64 ± 2.17 | 244.04 ± 1.63 | +30.98% |
| 256 | 2314.81 ± 33.43 | 1407.81 ± 14.15 | +64.43% | 302.86 ± 1.37 | 212.18 ± 2.60 | +42.74% |
| 512 | 2196.92 ± 15.75 | 1377.53 ± 5.74 | +59.48% | 272.71 ± 2.42 | 182.57 ± 2.79 | +49.37% |
| 1024 | 1986.98 ± 8.90 | 1329.53 ± 1.76 | +49.45% | 216.93 ± 0.78 | 144.61 ± 1.44 | +50.01% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
