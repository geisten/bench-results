# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2126.81 ± 30.80 | 1599.34 ± 12.79 | +32.98% | 116.26 ± 1.10 | 106.58 ± 0.48 | +9.09% |
| 256 | 2049.96 ± 25.68 | 1652.35 ± 5.15 | +24.06% | 114.28 ± 0.63 | 107.82 ± 0.71 | +5.99% |
| 512 | 1969.53 ± 21.04 | 1625.59 ± 13.30 | +21.16% | 110.63 ± 0.34 | 102.05 ± 0.57 | +8.41% |
| 1024 | 1862.64 ± 13.87 | 1521.47 ± 6.05 | +22.42% | 105.04 ± 0.36 | 91.88 ± 0.84 | +14.31% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
