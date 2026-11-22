# Current GPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 8608.81 ± 69.46 | 8298.56 ± 1409.86 | +3.74% | 357.98 ± 2.99 | 388.64 ± 2.69 | -7.89% |
| 256 | 11046.86 ± 15.75 | 13082.15 ± 169.80 | -15.56% | 355.73 ± 0.84 | 381.15 ± 3.34 | -6.67% |
| 512 | 13265.64 ± 24.06 | 14157.60 ± 82.10 | -6.30% | 347.11 ± 0.56 | 367.65 ± 2.97 | -5.59% |
| 1024 | 11888.80 ± 12.57 | 13212.25 ± 26.90 | -10.02% | 330.06 ± 0.95 | 349.98 ± 2.42 | -5.69% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
