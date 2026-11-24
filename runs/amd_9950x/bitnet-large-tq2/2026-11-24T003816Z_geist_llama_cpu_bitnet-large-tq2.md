# Current CPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `acaed04bf0f2`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2300.93 ± 271.01 | 1361.84 ± 1.37 | +68.96% | 322.18 ± 8.70 | 236.93 ± 2.70 | +35.98% |
| 256 | 2503.75 ± 82.19 | 1392.43 ± 14.31 | +79.81% | 306.41 ± 1.49 | 204.57 ± 2.85 | +49.78% |
| 512 | 2337.28 ± 35.56 | 1372.63 ± 3.67 | +70.28% | 271.28 ± 2.31 | 168.99 ± 3.44 | +60.53% |
| 1024 | 2097.57 ± 17.76 | 1323.18 ± 3.07 | +58.53% | 217.21 ± 3.76 | 126.33 ± 1.07 | +71.94% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
