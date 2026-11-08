# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9445.15 ± 31.04 | 10359.24 ± 1620.14 | -8.82% | 326.34 ± 2.39 | 388.31 ± 1.38 | -15.96% |
| 256 | 14023.56 ± 7.69 | 16249.65 ± 589.65 | -13.70% | 334.94 ± 0.67 | 357.28 ± 2.31 | -6.25% |
| 512 | 18374.30 ± 13.85 | 16753.80 ± 101.20 | +9.67% | 322.24 ± 0.13 | 343.38 ± 1.72 | -6.15% |
| 1024 | 16465.27 ± 64.03 | 15221.00 ± 48.80 | +8.17% | 312.19 ± 0.33 | 334.46 ± 2.82 | -6.66% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
