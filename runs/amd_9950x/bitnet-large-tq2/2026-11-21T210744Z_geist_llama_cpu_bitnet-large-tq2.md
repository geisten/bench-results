# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2505.54 ± 56.00 | 1360.29 ± 2.28 | +84.19% | 328.46 ± 2.46 | 250.20 ± 4.76 | +31.28% |
| 256 | 2483.05 ± 12.85 | 1390.42 ± 7.14 | +78.58% | 309.90 ± 2.83 | 218.51 ± 2.09 | +41.82% |
| 512 | 2307.16 ± 32.75 | 1373.15 ± 7.24 | +68.02% | 279.40 ± 3.16 | 187.90 ± 1.28 | +48.69% |
| 1024 | 2072.54 ± 24.80 | 1326.38 ± 1.76 | +56.26% | 222.44 ± 1.63 | 146.57 ± 0.51 | +51.76% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
