# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `e64ff1027649`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1869.12 ± 31.98 | 1346.20 ± 1.78 | +38.84% | 322.80 ± 2.03 | 242.10 ± 2.30 | +33.33% |
| 256 | 1827.99 ± 19.58 | 1376.15 ± 15.08 | +32.83% | 305.89 ± 1.55 | 213.78 ± 2.52 | +43.09% |
| 512 | 1751.68 ± 13.35 | 1339.62 ± 2.58 | +30.76% | 274.88 ± 1.30 | 185.03 ± 1.95 | +48.56% |
| 1024 | 1631.82 ± 16.54 | 1282.86 ± 6.25 | +27.20% | 218.74 ± 3.83 | 143.91 ± 1.23 | +51.99% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
