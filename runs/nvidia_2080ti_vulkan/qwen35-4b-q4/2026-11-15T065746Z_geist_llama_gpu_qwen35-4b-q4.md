# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2000.05 ± 7.80 | 2685.76 ± 4.85 | -25.53% | 131.50 ± 0.08 | 124.61 ± 0.16 | +5.52% |
| 256 | 3006.14 ± 3.22 | 3368.61 ± 4.58 | -10.76% | 131.21 ± 0.13 | 124.61 ± 0.19 | +5.30% |
| 512 | 3503.98 ± 2.03 | 3357.94 ± 6.29 | +4.35% | 130.94 ± 0.05 | 124.33 ± 0.10 | +5.32% |
| 1024 | 3465.72 ± 2.11 | 3321.84 ± 4.45 | +4.33% | 129.71 ± 0.07 | 122.60 ± 0.27 | +5.81% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
