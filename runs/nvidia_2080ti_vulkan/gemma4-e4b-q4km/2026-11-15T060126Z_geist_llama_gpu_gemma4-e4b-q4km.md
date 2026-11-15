# Current GPU head-to-head: geist vs llama.cpp

Model: `gemma4-e4b-Q4_K_M.gguf` (`85a896a047553e842f25297ee5b031d64ff30147d9c4af17b1e4b394cd1fab87`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1558.56 ± 2.05 | 2361.66 ± 4.39 | -34.01% | 99.45 ± 0.13 | 104.16 ± 0.16 | -4.53% |
| 256 | 2551.90 ± 3.41 | 3026.90 ± 7.76 | -15.69% | 98.57 ± 0.09 | 103.55 ± 0.16 | -4.81% |
| 512 | 2941.81 ± 13.10 | 3033.76 ± 5.10 | -3.03% | 98.09 ± 0.04 | 102.93 ± 0.24 | -4.71% |
| 1024 | 2897.17 ± 6.07 | 2841.65 ± 8.59 | +1.95% | 97.80 ± 0.04 | 102.39 ± 0.13 | -4.48% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
