# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `99e847f1c898`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2529.73 ± 82.44 | 1360.56 ± 3.92 | +85.93% | 326.80 ± 3.73 | 243.04 ± 2.27 | +34.46% |
| 256 | 2523.54 ± 31.78 | 1399.80 ± 9.28 | +80.28% | 308.73 ± 3.48 | 216.17 ± 2.40 | +42.82% |
| 512 | 2353.22 ± 15.83 | 1370.55 ± 3.71 | +71.70% | 274.18 ± 2.47 | 181.62 ± 3.44 | +50.97% |
| 1024 | 2078.94 ± 4.98 | 1325.72 ± 2.52 | +56.82% | 219.83 ± 3.96 | 143.94 ± 2.67 | +52.72% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
