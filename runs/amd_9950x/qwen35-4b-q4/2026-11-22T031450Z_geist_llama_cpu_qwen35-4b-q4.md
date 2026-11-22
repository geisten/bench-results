# Current CPU head-to-head: geist vs llama.cpp

Model: `qwen3.5-4b-q4_0.gguf` (`298fcb5fe7a77ccc79745ae24751560c5ac56874caff4bb39b1f2055bd72b8bb`)

geist `aeb3a50153d7`; llama.cpp `d81235049384`.

Host profile `amd_9950x`: 16-thread prefill, 15-thread decode, geist on `cpu_x86`, identical counts for both engines.

4 alternating A/B cycles, 3 raw samples per cell and cycle; median ± MAD. CPU-only, same model bytes, prompt/depth shapes and thread counts. Model loading is excluded.

Host: AMD Ryzen 9 9950X 16-Core Processor (16 physical cores), Linux 7.0.0-43-generic.

| Seq/depth | geist pp tok/s | llama.cpp pp tok/s | geist vs llama | geist tg tok/s | llama.cpp tg tok/s | geist vs llama |
| --: | --: | --: | --: | --: | --: | --: |
| 128 | 557.87 ± 7.23 | 305.67 ± 1.61 | +82.50% | 26.04 ± 0.10 | 23.39 ± 0.18 | +11.30% |
| 256 | 561.79 ± 5.19 | 314.06 ± 0.31 | +78.88% | 26.07 ± 0.07 | 23.28 ± 0.10 | +12.00% |
| 512 | 561.57 ± 4.60 | 310.73 ± 1.54 | +80.73% | 26.00 ± 0.04 | 23.13 ± 0.09 | +12.41% |
| 1024 | 560.88 ± 5.65 | 311.69 ± 1.94 | +79.95% | 25.91 ± 0.03 | 23.22 ± 0.10 | +11.57% |

Token streams are engine-native synthetic inputs; this is compute-shape parity, not token/logit parity. Publish speedups only together with the repository's separate quality-parity gate.
