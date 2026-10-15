# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `ebcdfb017ba6`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2360.51 ± 51.51 | 1358.76 ± 3.04 | +73.72% | 319.20 ± 1.54 | 239.76 ± 4.47 | +33.13% |
| 256 | 2333.06 ± 31.92 | 1410.16 ± 8.85 | +65.45% | 304.21 ± 2.89 | 208.77 ± 6.07 | +45.72% |
| 512 | 2220.29 ± 12.38 | 1380.78 ± 3.18 | +60.80% | 271.79 ± 2.35 | 183.64 ± 1.88 | +48.00% |
| 1024 | 2003.48 ± 15.45 | 1330.76 ± 3.09 | +50.55% | 215.04 ± 3.13 | 140.51 ± 3.24 | +53.05% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
