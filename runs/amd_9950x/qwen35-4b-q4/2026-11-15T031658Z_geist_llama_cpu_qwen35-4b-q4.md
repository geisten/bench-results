# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `7765b16fc97f`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 570.48 ± 4.22 | 309.00 ± 1.62 | +84.62% | 26.21 ± 0.04 | 23.41 ± 0.05 | +11.98% |
| 256 | 571.29 ± 5.80 | 316.26 ± 0.60 | +80.64% | 26.17 ± 0.03 | 23.46 ± 0.07 | +11.57% |
| 512 | 569.70 ± 1.10 | 316.88 ± 0.78 | +79.78% | 26.16 ± 0.10 | 23.32 ± 0.09 | +12.16% |
| 1024 | 561.98 ± 0.98 | 315.63 ± 1.67 | +78.05% | 26.13 ± 0.04 | 23.27 ± 0.08 | +12.25% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
