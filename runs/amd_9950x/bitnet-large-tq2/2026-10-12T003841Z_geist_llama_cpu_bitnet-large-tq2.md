# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `4d6e2696a51b`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2346.79 ± 45.45 | 1360.82 ± 2.99 | +72.46% | 321.67 ± 0.57 | 247.95 ± 1.79 | +29.74% |
| 256 | 2326.83 ± 19.98 | 1416.40 ± 11.36 | +64.28% | 305.12 ± 1.33 | 214.09 ± 1.77 | +42.52% |
| 512 | 2232.29 ± 17.11 | 1389.37 ± 5.05 | +60.67% | 276.64 ± 1.61 | 186.32 ± 0.92 | +48.48% |
| 1024 | 2010.85 ± 6.33 | 1333.24 ± 3.49 | +50.82% | 217.93 ± 0.70 | 146.31 ± 0.96 | +48.95% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
