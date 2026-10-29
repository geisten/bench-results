# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `1515c60147c9`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 393.38 ± 4.32 | 270.63 ± 0.69 | +45.36% | 26.02 ± 0.05 | 23.06 ± 0.08 | +12.85% |
| 256 | 397.05 ± 4.64 | 274.40 ± 0.26 | +44.70% | 25.98 ± 0.09 | 23.04 ± 0.06 | +12.74% |
| 512 | 397.89 ± 3.73 | 281.89 ± 6.73 | +41.15% | 25.91 ± 0.08 | 22.89 ± 0.09 | +13.16% |
| 1024 | 398.21 ± 2.16 | 273.97 ± 0.73 | +45.35% | 25.80 ± 0.07 | 22.75 ± 0.05 | +13.40% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
