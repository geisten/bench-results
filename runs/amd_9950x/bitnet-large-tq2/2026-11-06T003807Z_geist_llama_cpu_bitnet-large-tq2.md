# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `49ffbf5118ee`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2587.61 ± 24.48 | 1360.86 ± 4.07 | +90.15% | 320.63 ± 2.18 | 241.24 ± 1.76 | +32.91% |
| 256 | 2556.08 ± 26.33 | 1422.50 ± 5.50 | +79.69% | 304.55 ± 2.39 | 213.63 ± 1.69 | +42.56% |
| 512 | 2385.93 ± 11.39 | 1394.37 ± 2.50 | +71.11% | 272.65 ± 1.76 | 185.07 ± 0.59 | +47.32% |
| 1024 | 2114.33 ± 16.40 | 1332.56 ± 3.46 | +58.67% | 215.58 ± 1.64 | 144.76 ± 1.00 | +48.92% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
