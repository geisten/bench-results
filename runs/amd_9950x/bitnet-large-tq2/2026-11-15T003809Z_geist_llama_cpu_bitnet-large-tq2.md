# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2591.70 ± 36.66 | 1361.01 ± 2.61 | +90.42% | 321.22 ± 5.19 | 242.32 ± 2.93 | +32.56% |
| 256 | 2556.88 ± 22.61 | 1420.16 ± 8.55 | +80.04% | 302.74 ± 4.89 | 220.94 ± 1.27 | +37.02% |
| 512 | 2397.65 ± 12.52 | 1390.89 ± 5.41 | +72.38% | 267.70 ± 0.91 | 190.12 ± 1.34 | +40.81% |
| 1024 | 2120.63 ± 9.96 | 1335.19 ± 1.61 | +58.83% | 219.17 ± 4.21 | 146.08 ± 1.78 | +50.03% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
