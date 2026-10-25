# Current GPU head-to-head: geist vs llama.cpp

Model: `bitnet_b1_58-large-TQ2_0.gguf` (`281aafb18a9f4a3124c10a1d8683e2296f0cfe8a2944da0a5667d17488a951bb`)

geist `af6689407a1d`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on AMD Ryzen 9 9950X 16-Core Processor (RADV RAPHAEL_MENDOCINO), same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 92.39 ± 0.04 | 275.41 ± 0.11 | -66.45% | 36.00 ± 0.02 | 65.75 ± 0.05 | -45.26% |
| 256 | 84.62 ± 0.02 | 274.10 ± 0.08 | -69.13% | 39.80 ± 0.01 | 64.23 ± 0.05 | -38.04% |
| 512 | 70.97 ± 0.01 | 274.07 ± 0.04 | -74.11% | 38.31 ± 0.00 | 61.26 ± 0.12 | -37.47% |
| 1024 | 52.24 ± 0.07 | 266.20 ± 0.03 | -80.38% | 31.44 ± 0.01 | 55.81 ± 0.06 | -43.67% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
