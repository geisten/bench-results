# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `666d971e5db2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2517.87 ± 60.12 | 1362.59 ± 3.00 | +84.79% | 325.73 ± 4.48 | 241.02 ± 2.04 | +35.15% |
| 256 | 2527.91 ± 35.91 | 1424.28 ± 11.05 | +77.49% | 308.50 ± 4.06 | 219.93 ± 1.07 | +40.27% |
| 512 | 2367.56 ± 18.47 | 1392.92 ± 2.38 | +69.97% | 275.94 ± 3.68 | 190.62 ± 2.13 | +44.76% |
| 1024 | 2105.45 ± 13.39 | 1337.67 ± 1.04 | +57.40% | 218.07 ± 3.24 | 145.80 ± 1.62 | +49.57% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
