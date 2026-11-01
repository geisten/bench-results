# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9472.01 ± 12.99 | 10359.85 ± 1575.68 | -8.57% | 328.19 ± 2.14 | 389.97 ± 1.10 | -15.84% |
| 256 | 13997.10 ± 17.60 | 16826.15 ± 194.50 | -16.81% | 335.73 ± 0.82 | 355.96 ± 2.69 | -5.68% |
| 512 | 18379.58 ± 18.14 | 16885.15 ± 80.55 | +8.85% | 323.36 ± 0.21 | 342.82 ± 3.64 | -5.68% |
| 1024 | 16523.99 ± 33.98 | 15300.45 ± 35.40 | +8.00% | 312.84 ± 0.75 | 333.88 ± 1.92 | -6.30% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
