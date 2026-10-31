# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `93817e73fce2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2560.27 ± 61.59 | 1364.79 ± 6.32 | +87.59% | 320.77 ± 9.31 | 244.83 ± 3.40 | +31.02% |
| 256 | 2559.21 ± 18.37 | 1431.95 ± 3.71 | +78.72% | 310.32 ± 1.50 | 215.45 ± 2.05 | +44.03% |
| 512 | 2399.95 ± 19.53 | 1401.11 ± 2.29 | +71.29% | 277.31 ± 2.21 | 184.99 ± 1.01 | +49.91% |
| 1024 | 2142.00 ± 18.17 | 1337.62 ± 2.76 | +60.13% | 216.84 ± 3.12 | 146.81 ± 1.14 | +47.70% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
