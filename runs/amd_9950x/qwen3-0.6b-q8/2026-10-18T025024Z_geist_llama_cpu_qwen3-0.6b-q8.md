# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 2026.04 ± 53.52 | 1591.71 ± 19.11 | +27.29% | 116.80 ± 0.70 | 105.46 ± 0.77 | +10.75% |
| 256 | 2049.98 ± 33.55 | 1653.15 ± 10.12 | +24.00% | 115.92 ± 0.34 | 106.69 ± 0.50 | +8.65% |
| 512 | 1985.21 ± 27.97 | 1630.37 ± 5.61 | +21.76% | 112.01 ± 0.45 | 101.45 ± 0.42 | +10.41% |
| 1024 | 1861.47 ± 13.13 | 1517.70 ± 5.32 | +22.65% | 105.41 ± 0.14 | 91.21 ± 0.89 | +15.56% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
