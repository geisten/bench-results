# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2108.06 ± 69.68 | 1626.91 ± 5.05 | +29.57% | 116.37 ± 0.88 | 104.67 ± 0.45 | +11.18% |
| 256 | 2107.13 ± 34.68 | 1669.44 ± 6.16 | +26.22% | 113.55 ± 0.43 | 105.70 ± 1.65 | +7.43% |
| 512 | 1997.87 ± 21.65 | 1670.03 ± 6.00 | +19.63% | 109.53 ± 0.18 | 99.10 ± 1.01 | +10.53% |
| 1024 | 1881.32 ± 9.89 | 1541.53 ± 3.26 | +22.04% | 104.11 ± 0.22 | 90.14 ± 0.16 | +15.50% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
