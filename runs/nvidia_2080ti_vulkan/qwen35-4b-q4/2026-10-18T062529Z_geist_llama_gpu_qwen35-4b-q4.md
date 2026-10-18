# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2003.68 ± 2.94 | 2691.97 ± 3.95 | -25.57% | 122.88 ± 0.05 | 125.12 ± 0.17 | -1.79% |
| 256 | 3011.71 ± 2.87 | 3367.33 ± 7.01 | -10.56% | 122.79 ± 0.11 | 124.98 ± 0.24 | -1.76% |
| 512 | 3523.17 ± 2.86 | 3369.16 ± 2.28 | +4.57% | 122.29 ± 0.09 | 124.34 ± 0.39 | -1.65% |
| 1024 | 3485.54 ± 2.18 | 3321.72 ± 8.32 | +4.93% | 121.37 ± 0.13 | 122.44 ± 0.11 | -0.87% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
