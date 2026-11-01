# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1986.73 ± 2.25 | 2694.03 ± 6.25 | -26.25% | 122.77 ± 0.19 | 124.83 ± 0.16 | -1.65% |
| 256 | 2991.62 ± 2.89 | 3374.53 ± 12.09 | -11.35% | 122.70 ± 0.07 | 124.50 ± 0.10 | -1.45% |
| 512 | 3495.13 ± 3.38 | 3359.39 ± 3.44 | +4.04% | 122.38 ± 0.07 | 124.35 ± 0.20 | -1.59% |
| 1024 | 3457.27 ± 3.36 | 3320.14 ± 5.05 | +4.13% | 121.35 ± 0.11 | 122.12 ± 0.23 | -0.63% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
