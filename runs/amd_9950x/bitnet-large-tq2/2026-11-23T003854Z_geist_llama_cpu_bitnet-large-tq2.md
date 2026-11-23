# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `b90b6b27c840`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2545.25 ± 67.30 | 1359.19 ± 3.15 | +87.26% | 331.25 ± 2.26 | 242.70 ± 1.72 | +36.49% |
| 256 | 2476.09 ± 21.98 | 1402.53 ± 13.97 | +76.54% | 310.95 ± 2.34 | 205.51 ± 2.42 | +51.30% |
| 512 | 2327.41 ± 39.77 | 1370.89 ± 10.77 | +69.77% | 275.93 ± 4.28 | 171.40 ± 4.01 | +60.99% |
| 1024 | 2081.06 ± 16.39 | 1322.56 ± 4.31 | +57.35% | 222.25 ± 3.20 | 126.65 ± 1.07 | +75.49% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
