# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `6642260d55a1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 560.25 ± 6.29 | 309.59 ± 1.58 | +80.97% | 26.26 ± 0.04 | 23.55 ± 0.10 | +11.53% |
| 256 | 557.02 ± 7.20 | 316.75 ± 1.11 | +75.86% | 26.27 ± 0.06 | 23.19 ± 0.11 | +13.30% |
| 512 | 560.82 ± 2.72 | 317.00 ± 1.59 | +76.92% | 26.24 ± 0.06 | 23.31 ± 0.07 | +12.58% |
| 1024 | 555.32 ± 5.84 | 313.37 ± 1.64 | +77.21% | 26.16 ± 0.07 | 22.88 ± 0.08 | +14.34% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
