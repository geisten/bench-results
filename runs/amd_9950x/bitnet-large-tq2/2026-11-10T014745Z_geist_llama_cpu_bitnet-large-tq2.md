# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `29a0ce4b5937`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2602.87 ± 22.62 | 1363.32 ± 1.45 | +90.92% | 334.12 ± 2.38 | 251.72 ± 4.84 | +32.74% |
| 256 | 2566.62 ± 20.73 | 1422.05 ± 4.90 | +80.49% | 313.84 ± 1.66 | 217.21 ± 1.26 | +44.49% |
| 512 | 2361.41 ± 17.88 | 1393.91 ± 3.75 | +69.41% | 281.97 ± 3.36 | 186.60 ± 2.71 | +51.11% |
| 1024 | 2101.92 ± 17.66 | 1333.95 ± 2.82 | +57.57% | 223.44 ± 4.19 | 146.59 ± 1.11 | +52.42% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
