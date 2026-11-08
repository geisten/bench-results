# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2575.82 ± 22.96 | 1358.87 ± 6.91 | +89.56% | 326.71 ± 3.50 | 248.25 ± 3.80 | +31.60% |
| 256 | 2561.63 ± 35.50 | 1421.45 ± 10.62 | +80.21% | 305.76 ± 0.78 | 213.15 ± 2.71 | +43.45% |
| 512 | 2366.44 ± 12.65 | 1396.67 ± 8.94 | +69.43% | 274.20 ± 2.48 | 184.40 ± 0.68 | +48.69% |
| 1024 | 2112.09 ± 10.49 | 1340.91 ± 4.57 | +57.51% | 220.43 ± 3.27 | 145.96 ± 1.44 | +51.02% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
