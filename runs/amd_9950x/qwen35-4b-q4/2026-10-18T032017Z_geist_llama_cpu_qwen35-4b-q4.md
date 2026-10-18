# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `c993379b0746`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-38-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 553.13 ± 3.67 | 305.63 ± 0.91 | +80.98% | 26.10 ± 0.08 | 23.29 ± 0.07 | +12.06% |
| 256 | 552.32 ± 4.48 | 313.58 ± 1.40 | +76.13% | 26.10 ± 0.07 | 23.35 ± 0.12 | +11.80% |
| 512 | 554.83 ± 3.71 | 298.43 ± 6.12 | +85.92% | 26.08 ± 0.05 | 23.25 ± 0.20 | +12.21% |
| 1024 | 545.95 ± 3.70 | 304.30 ± 4.21 | +79.41% | 25.88 ± 0.06 | 23.08 ± 0.10 | +12.12% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
