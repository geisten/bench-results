# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9448.59 ± 34.30 | 10422.70 ± 1617.75 | -9.35% | 326.43 ± 2.28 | 389.62 ± 1.69 | -16.22% |
| 256 | 14010.13 ± 19.56 | 16800.85 ± 204.85 | -16.61% | 333.74 ± 0.97 | 351.93 ± 0.64 | -5.17% |
| 512 | 18366.40 ± 22.04 | 16765.15 ± 34.75 | +9.55% | 320.41 ± 1.18 | 342.32 ± 1.41 | -6.40% |
| 1024 | 16552.84 ± 15.52 | 15269.05 ± 28.35 | +8.41% | 312.29 ± 0.66 | 332.45 ± 2.73 | -6.07% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
