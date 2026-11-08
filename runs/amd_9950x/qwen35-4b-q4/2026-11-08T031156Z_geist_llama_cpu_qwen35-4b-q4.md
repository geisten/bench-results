# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `ff31d42364e1`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 569.00 ± 5.16 | 311.18 ± 1.62 | +82.85% | 26.17 ± 0.07 | 23.21 ± 0.06 | +12.78% |
| 256 | 569.62 ± 2.16 | 317.40 ± 0.58 | +79.47% | 26.15 ± 0.05 | 23.17 ± 0.07 | +12.83% |
| 512 | 569.43 ± 2.97 | 316.82 ± 2.86 | +79.74% | 26.11 ± 0.06 | 23.28 ± 0.13 | +12.14% |
| 1024 | 566.08 ± 3.71 | 313.81 ± 1.92 | +80.39% | 26.04 ± 0.03 | 23.13 ± 0.05 | +12.57% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
