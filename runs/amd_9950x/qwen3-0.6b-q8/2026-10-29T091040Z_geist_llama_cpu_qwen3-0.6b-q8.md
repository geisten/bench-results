# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3-0.6b-q8_0.gguf` (`9465e63a22add5354d9bb4b99e90117043c7124007664907259bd16d043bb031`)

geist `7458b37b9531`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 1448.02 ± 48.61 | 1137.85 ± 17.35 | +27.26% | 113.48 ± 2.12 | 104.64 ± 0.67 | +8.45% |
| 256 | 1464.54 ± 34.08 | 1167.07 ± 23.51 | +25.49% | 110.65 ± 1.83 | 105.01 ± 1.20 | +5.37% |
| 512 | 1427.82 ± 14.90 | 1153.50 ± 9.52 | +23.78% | 107.65 ± 0.76 | 98.88 ± 0.85 | +8.87% |
| 1024 | 1358.37 ± 15.20 | 1093.42 ± 7.96 | +24.23% | 101.33 ± 1.12 | 89.87 ± 0.36 | +12.75% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
