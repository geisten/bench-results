# Current GPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `nvidia_2080ti_vulkan`: 4-thread prefill, 4-thread decode, geist on `vulkan`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. Full GPU offload on NVIDIA GeForce RTX 2080 Ti, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 9583.35 ± 53.75 | 10390.05 ± 1635.10 | -7.76% | 349.63 ± 1.40 | 389.81 ± 0.68 | -10.31% |
| 256 | 14223.80 ± 11.07 | 14585.00 ± 2297.40 | -2.48% | 356.75 ± 0.27 | 359.24 ± 1.47 | -0.69% |
| 512 | 18888.46 ± 12.53 | 16781.70 ± 41.40 | +12.55% | 341.34 ± 0.15 | 347.48 ± 2.77 | -1.77% |
| 1024 | 16959.54 ± 9.55 | 15219.75 ± 44.30 | +11.43% | 331.95 ± 0.05 | 336.55 ± 1.58 | -1.37% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
