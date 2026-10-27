# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `df665fe9c736`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1848.73 ± 56.53 | 1271.58 ± 38.67 | +45.39% | 305.67 ± 9.42 | 235.20 ± 3.92 | +29.96% |
| 256 | 1797.38 ± 20.88 | 1322.05 ± 47.41 | +35.95% | 289.17 ± 3.39 | 211.78 ± 2.93 | +36.54% |
| 512 | 1722.44 ± 25.82 | 1258.47 ± 21.90 | +36.87% | 257.32 ± 2.12 | 183.48 ± 1.65 | +40.24% |
| 1024 | 1575.55 ± 20.29 | 1204.53 ± 7.61 | +30.80% | 208.98 ± 3.22 | 143.73 ± 1.15 | +45.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
