# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `0894d5e63e09`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9361.86 ± 93.71 | 10385.34 ± 1644.51 | -9.86% | 325.36 ± 1.78 | 389.96 ± 0.95 | -16.56% |
| 256 | 13976.86 ± 27.09 | 16815.40 ± 177.50 | -16.88% | 332.41 ± 1.09 | 353.25 ± 1.98 | -5.90% |
| 512 | 18336.80 ± 26.31 | 16775.40 ± 62.05 | +9.31% | 319.52 ± 0.14 | 343.83 ± 2.21 | -7.07% |
| 1024 | 16526.79 ± 18.41 | 15201.60 ± 52.10 | +8.72% | 310.58 ± 0.10 | 334.48 ± 2.42 | -7.14% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
