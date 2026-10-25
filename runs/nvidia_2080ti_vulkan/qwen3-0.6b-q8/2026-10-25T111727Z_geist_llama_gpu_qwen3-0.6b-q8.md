# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `d95bf356d2f7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on AMD Ryzen 9 9950X 16-Core Processor (RADV RAPHAEL_MENDOCINO), same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 106.60 ± 0.02 | 383.66 ± 0.07 | -72.22% | 55.61 ± 0.03 | 62.84 ± 0.03 | -11.51% |
| 256 | 91.64 ± 0.02 | 380.47 ± 0.05 | -75.91% | 62.36 ± 0.03 | 61.53 ± 0.03 | +1.34% |
| 512 | 69.66 ± 0.08 | 379.20 ± 0.02 | -81.63% | 57.50 ± 0.04 | 59.48 ± 0.04 | -3.34% |
| 1024 | 45.46 ± 0.08 | 360.19 ± 0.09 | -87.38% | 51.96 ± 0.03 | 55.89 ± 0.04 | -7.03% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
