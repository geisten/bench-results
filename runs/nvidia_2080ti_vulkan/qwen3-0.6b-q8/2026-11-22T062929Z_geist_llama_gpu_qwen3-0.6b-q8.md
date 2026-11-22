# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9608.89 ± 52.95 | 10443.51 ± 1641.98 | -7.99% | 354.02 ± 0.81 | 392.70 ± 1.04 | -9.85% |
| 256 | 14229.34 ± 7.91 | 16594.00 ± 498.85 | -14.25% | 359.84 ± 0.33 | 351.43 ± 2.75 | +2.39% |
| 512 | 18926.86 ± 7.35 | 16876.10 ± 69.00 | +12.15% | 344.67 ± 0.22 | 344.75 ± 5.64 | -0.03% |
| 1024 | 16952.66 ± 19.37 | 15260.80 ± 49.10 | +11.09% | 334.70 ± 0.20 | 334.46 ± 4.51 | +0.07% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
